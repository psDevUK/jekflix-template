---
date: 2019-12-03 12:00:00
layout: post
title: Serving SQL on a UniversalDashboard
subtitle: Showing how to display SQL output in Powershell UniversalDashboard.
description: This blog covers how to output data from SQL to a Powershell UniversalDashboard to either display charts or datagrids of information.
image: https://cdn.lynda.com/course/139988/139988-637021525148800194-16x9.jpg
optimized_image: https://cdn.lynda.com/course/139988/139988-637021525148800194-16x9.jpg
category: SQL
tags:
  - SQL
  - UD
  - cookbook
author: psdevuk
---

# SQL

First off I just want to point out I am not a master of SQL but I can construct numerous tpyes of SQL queries or stored procedures to return the required data. Then displaying that data in a powershell universal dashboard. Before I found this amazing product, I used to use excel, and then put that data into a pivot table or a chart. Although this was ok, it still took time to run the macro to display the data, and Excel is pretty **intensive** on your PC if you are loading lots of data, and can therefore take a while to process all this data

> SQL and Powershell UniversalDashboard go together like butter on hot toast. It is such a good tool to use to display SQL data.

Please do take the time to have a butchers at my blog on the **projects** I have done with powershell universaldashboard as these are all using SQL data in the back-end and the beautiful looking front-end is the awesome powershell universaldashboard.

## Hold up...

Please remember to <a href="https://docs.universaldashboard.io/">check the official documentation page</a> as the author for this project, the very talented Adam Driscoll has done an amazing job not only building and deploying this product to the general public, but also documenting it, and how it all works.

## Lets get started

> Whenever I am using SQL on universaldashboard <a href= "https://gallery.technet.microsoft.com/ScriptCenter/7985b7ef-ed89-4dfd-b02a-433cc4e30894">I use the following module here</a>. If you do not have it already and you want to follow along then go get your copy now. This is a pretty old but reliable function I have used for years.

So I am assuming that you can write basic SQL queries to return data, as these blogs are dedicated to **powershell universaldashboard** so without further a-do lets get started.

Hopefully you had a gander at the official documentation and looked at how to load functions into your dashboard. As when I first got using this product, I was being a douche-bag and placing the whole function inside every single `-Content` or `-Endpoint` script block as I didn't understand how to make my function be loaded just once and be used throughout my dashbaord, as in just calling the function name to run the function. As placing the whole function code block numerous times throughout your script, does make one super-long script. So please do not use that method of placing the entire function in each script block.

Instead I should have been doing this, and this is how I roll now:-

```
function Invoke-Sqlcmd2 {
    [CmdletBinding()]
    param (
        [Parameter(Position = 0, Mandatory = $true)]
        [string]$ServerInstance,
        [Parameter(Position = 1, Mandatory = $false)]
        [string]$Database,
        [Parameter(Position = 2, Mandatory = $false)]
        [string]$Query,
        [Parameter(Position = 3, Mandatory = $false)]
        [string]$Username,
        [Parameter(Position = 4, Mandatory = $false)]
        [string]$Password,
        [Parameter(Position = 5, Mandatory = $false)]
        [Int32]$QueryTimeout = 600,
        [Parameter(Position = 6, Mandatory = $false)]
        [Int32]$ConnectionTimeout = 15,
        [Parameter(Position = 7, Mandatory = $false)]
        [ValidateScript( { test-path $_ })]
        [string]$InputFile,
        [Parameter(Position = 8, Mandatory = $false)]
        [ValidateSet("DataSet", "DataTable", "DataRow")]
        [string]$As = "DataRow"
    )

    if ($InputFile) {
        $filePath = $(resolve-path $InputFile).path
        $Query = [System.IO.File]::ReadAllText("$filePath")
    }

    $conn = new-object System.Data.SqlClient.SQLConnection

    if ($Username)
    { $ConnectionString = "Server={0};Database={1};User ID={2};Password={3};Trusted_Connection=False;Connect Timeout={4}" -f $ServerInstance, $Database, $Username, $Password, $ConnectionTimeout }
    else
    { $ConnectionString = "Server={0};Database={1};Integrated Security=True;Connect Timeout={2}" -f $ServerInstance, $Database, $ConnectionTimeout }

    $conn.ConnectionString = $ConnectionString

    #Following EventHandler is used for PRINT and RAISERROR T-SQL statements. Executed when -Verbose parameter specified by caller
    if ($PSBoundParameters.Verbose) {
        $conn.FireInfoMessageEventOnUserErrors = $true
        $handler = [System.Data.SqlClient.SqlInfoMessageEventHandler] { Write-Verbose "$($_)" }
        $conn.add_InfoMessage($handler)
    }

    $conn.Open()
    $cmd = new-object system.Data.SqlClient.SqlCommand($Query, $conn)
    $cmd.CommandTimeout = $QueryTimeout
    $ds = New-Object system.Data.DataSet
    $da = New-Object system.Data.SqlClient.SqlDataAdapter($cmd)
    [void]$da.fill($ds)
    $conn.Close()
    switch ($As) {
        'DataSet' { Write-Output ($ds) }
        'DataTable' { Write-Output ($ds.Tables) }
        'DataRow' { Write-Output ($ds.Tables[0]) }
    }

}
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDNumber
$Init = New-UDEndpointInitialization -Function @("Invoke-Sqlcmd2") -Module @("UniversalDashboard.UDNumber")
$dashboard = New-UDDashboard -Title "SQL on a Dashboard" -EndpointInitialization $Init  -Content {
    New-UDRow -Columns {
        New-UDColumn -Size 6 -Endpoint {
            New-UDCard -Content {
                 $qCount = @"
SELECT COUNT(M.EmployeeID) Complaints
FROM [COMPLAINT].[dbo].[Main] as M
INNER JOIN COMPLAINT.dbo.Employee E ON M.EmployeeID = E.EmployeeID
WHERE E.SamAccountName = '$($User)'
"@
$Session:MyNum = Invoke-Sqlcmd2 -ServerInstance SQL-SERVER -Database COMPLAINT -Query $qCount -Username username -Password password | select-object -ExpandProperty Complaints

        New-UDNumber -End $Session:MyNum -Delay 5 -PreFix "Complaints Raised"
            }
        } -AutoRefresh -RefreshInterval 20
    }
}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```

This is a complete dashboard! Lets note some important things here. First thing I did was to use place the function at the top of my script block, I then imported the universaldashboard module, then I imported a custom component module I built which I blogged about previously. So **two** custom things need to be imported into my universaldashboard session, a custom fuction and a custom module. This was done by using `$Init = New-UDEndpointInitialization -Function @("Invoke-Sqlcmd2") -Module @("UniversalDashboard.UDNumber")` to hold the **custom function and custom module** then if you look carefully I am binding the variable I initialised to hold this information in, into the `-EndpointInitialization` parameter on the dashboard.

This now means I can use `invoke-sqlcmd2` and `new-udcounter` anywhere I want in my dashboard. Cool beans. So moving on you see I chose to display the output from SQL into a card component, in that card component it will display the number of complaints I have raised.

But how did I dynamically get **my complaints**? Simple, as this dashboard is linked to a login page with authentication (**this is not shown in the example**) that means I can use the `$user` variable which holds the current username of the person logged in. I then refrence that username in a **WHERE** clause of my SQL query to get me my complaints.

The other important thing to note in this script block is the use of the `$Session` variable which is used to store the number of complaints I have raised. More information on the session variable scope can be found in the official documentation, but this variable is storing this variable per session which is established once the user is connected to the dashboard. I used this as I am calling this same session variable in other endpoints on my official script.

I only wanted to display the number from the SQL query not the column heading and the number, so this is why I piped the `invoke-sqlcmd2` command to `select-object -ExpandProperty Complaints` as now I am only returned the number.

That is in a nutshell how you obtain SQL data in powershell universaldashboard. But why stop there when I feel I have just started...

## Displaying in UDGrid

So the first way I like to display my data is to use the `new-udgrid` command which will look something like <a href="https://poshud.com/New-UDGrid">this</a>

I believe the technology used to display the output for `New-UDGrid` is using griddle. This displays the data in a grid fashion and has a live dynamic search bar at the top of the grid which can be used to filter the results. It also has the ability to display the data in ascending or descending format on any chosen column. So again referencing the complaint database I built to show me in udgrid format all of the complaints I have raised

```
         New-UDGrid -Id "mCalls" -Title "My Complaints" -Headers @("ID", "Account", "Depot", "Status", "Problem", "Product", "Incident", "Assigned", "Logged") -Properties @("ComplaintID", "AccountName", "DepotName", "StatusSituation", "ProblemType", "ProductName", "IncidentDate", "AssignedTo", "LoggedDate") -DefaultSortColumn "ComplaintID" -PageSize 10  -Endpoint {
                $qMyCalls = @"
            SELECT M.ComplaintID
                  ,CC.AccountName
                  ,C.DepotName
                  ,S.StatusSituation
                  ,PR.ProblemType
                  ,P.ProductName
                  ,[Description]
                  ,[IncidentDate]
                  ,COUNT(A.AttachmentName) [Attachments]
                  ,E.DisplayName AS RaisedBy
                  ,E2.DisplayName AS AssignedTo
                  ,[DeliveryRef]
                  ,[LoggedDate]
              FROM [COMPLAINT].[dbo].[Main] as M
              INNER JOIN COMPLAINT.dbo.Depot as C ON M.DepotID = C.DepotID
              INNER JOIN COMPLAINT.dbo.Employee E ON M.EmployeeID = E.EmployeeID
              INNER JOIN COMPLAINT.dbo.Employee E2 ON M.AssignedTo = E2.EmployeeID
              LEFT JOIN COMPLAINT.dbo.Product P ON M.ProductID = P.ProductID
              INNER JOIN COMPLAINT.dbo.Problem PR on M.ProblemID = PR.ProblemID
              INNER JOIN COMPLAINT.dbo.Status S ON M.StatusID = S.StatusID
              INNER JOIN COMPLAINT.dbo.Customer CC ON M.CustomerID = CC.CustomerID
            LEFT JOIN COMPLAINT.dbo.Attachment A ON M.ComplaintID = A.ComplaintID
             WHERE E.SamAccountName = '$($User)'
            GROUP BY M.ComplaintID
                  ,CC.AccountName
                  ,C.DepotName
                  ,S.StatusSituation
                  ,PR.ProblemType
                  ,P.ProductName
                  ,[Description]
                  ,[IncidentDate]
                  ,E.DisplayName
                  ,[DeliveryRef]
                  ,[LoggedDate]
                  ,E2.DisplayName
"@
                $CallData = Invoke-Sqlcmd2 -ServerInstance SQL-SERVER -Database COMPLAINT -Query $qMyCalls -Username username -Password password
                $CallData | Select-Object "ComplaintID", "AccountName", "DepotName", "StatusSituation", "ProblemType", "ProductName", "IncidentDate", "AssignedTo", "LoggedDate" | Out-UDGridData
            } -AutoRefresh -RefreshInterval 20
```

This will automatically refresh the grid every 20 seconds, as these are react components, they can refresh themself on the page, which means no more **F5** to get the latest results, as this is automatically refreshing for me, without the blip in the load time. Very nice.

I hope that more grids come to universaldashboard as I would like to see more capability added to the grid to get it to display more in a pivot table manner.

Anyways this is `new-udgrid` and is great for displaying data from SQL. This also now includes a built-in pre-loader so that when the user is waiting they do get a progress bar

## Cache big data

So in my job for one of the many databases I connect to, I have to use a given **public** database of the actual database, which only contains views. So this does limit me to having to use the given view to obtain the required data. Now this wouldn't be a problem if it didn't take over a minute sometimes to get data that I feel should take 10 seconds or less in SQL. But as mentioned I am limited to the access I have in this particular database.

Now you may think that I am just on a moan and rant, well yes kind of, but there is a reason behind this. I bring you the solution which is to **cache big data** to get it to display a lot quicker on your dashboard.

You can set timed intervals to refresh what data you are holding in the cache data. This is a special variable for universaldashboard and can be used throughout your entire dashboard as well which is pretty damn neat. As mentioned you can set timed intervals for the cached data to be refreshed, which in-turn dynamically refreshes this throughout your dashboard where you are calling this.

I do not believe it is officially documented anywhere and this is personal preference as well, but I like to split my dashboard into separate script files, one for each menu page. Not only does this make my code loads easier to troubleshoot, maintain and update. This also makes the individual script files pretty small. So when I do use the `$cache` variable create your own script file to hold all this information in. An example on splitting a dashboard into multiple files <a href="https://github.com/psDevUK/psUniversalDashboard/blob/master/FleetManagementGitHub.ps1">look at this link</a>

```
$Schedule = New-UDEndpointSchedule -Every 200 -Second
New-UDEndpoint -Schedule $Schedule -Endpoint {
    function Invoke-Sqlcmd2 {
        [CmdletBinding()]
        param (
            [Parameter(Position = 0, Mandatory = $true)]
            [string]$ServerInstance,
            [Parameter(Position = 1, Mandatory = $false)]
            [string]$Database,
            [Parameter(Position = 2, Mandatory = $false)]
            [string]$Query,
            [Parameter(Position = 3, Mandatory = $false)]
            [string]$Username,
            [Parameter(Position = 4, Mandatory = $false)]
            [string]$Password,
            [Parameter(Position = 5, Mandatory = $false)]
            [Int32]$QueryTimeout = 600,
            [Parameter(Position = 6, Mandatory = $false)]
            [Int32]$ConnectionTimeout = 15,
            [Parameter(Position = 7, Mandatory = $false)]
            [ValidateScript( { test-path $_ })]
            [string]$InputFile,
            [Parameter(Position = 8, Mandatory = $false)]
            [ValidateSet("DataSet", "DataTable", "DataRow")]
            [string]$As = "DataRow"
        )

        if ($InputFile) {
            $filePath = $(resolve-path $InputFile).path
            $Query = [System.IO.File]::ReadAllText("$filePath")
        }

        $conn = new-object System.Data.SqlClient.SQLConnection

        if ($Username)
        { $ConnectionString = "Server={0};Database={1};User ID={2};Password={3};Trusted_Connection=False;Connect Timeout={4}" -f $ServerInstance, $Database, $Username, $Password, $ConnectionTimeout }
        else
        { $ConnectionString = "Server={0};Database={1};Integrated Security=True;Connect Timeout={2}" -f $ServerInstance, $Database, $ConnectionTimeout }

        $conn.ConnectionString = $ConnectionString

        #Following EventHandler is used for PRINT and RAISERROR T-SQL statements. Executed when -Verbose parameter specified by caller
        if ($PSBoundParameters.Verbose) {
            $conn.FireInfoMessageEventOnUserErrors = $true
            $handler = [System.Data.SqlClient.SqlInfoMessageEventHandler] { Write-Verbose "$($_)" }
            $conn.add_InfoMessage($handler)
        }

        $conn.Open()
        $cmd = new-object system.Data.SqlClient.SqlCommand($Query, $conn)
        $cmd.CommandTimeout = $QueryTimeout
        $ds = New-Object system.Data.DataSet
        $da = New-Object system.Data.SqlClient.SqlDataAdapter($cmd)
        [void]$da.fill($ds)
        $conn.Close()
        switch ($As) {
            'DataSet' { Write-Output ($ds) }
            'DataTable' { Write-Output ($ds.Tables) }
            'DataRow' { Write-Output ($ds.Tables[0]) }
        }

    }
    $SuperLongQuery = @"
Select Vehicle_ID,
UPPER([Registration]) Registration
FROM YourDB.dbo.Vehicle
WHERE Active_ID = 1
"@
    $Cache:BigData = Invoke-Sqlcmd2 -ServerInstance SQL-SERVER -Database YourDB -Query $SuperLongQuery -Username username -Password password
}
```

So in the above script block I could of added loads more queries and `$Cache:AnotherVariable` to use to hold more data. In the above example, we are assuming the query would take 30 seconds or more to display these results. So to prevent this taking that amount of time for when a user lands on a page, we are now hold this long time consuming query into a `$Cache` variable which will be updated every 200 seconds.

So if you have not done so already please read up on the `$cache` variable on the official document site.

## Chart Example

So just to finish off with, here is how you could present the information from your SQL query into a chart. In this example I am displaying how many complaints each depot has raised

```
New-UDChart -Type Bar -Title "Complaints By Depot" -BackgroundColor "#1e353f" -FontColor "#ffffff" -Endpoint {

$qtotals = @"
SELECT COUNT(D.DepotID) Total
,D.DepotName
FROM [COMPLAINT].[dbo].[Main] as M
INNER JOIN COMPLAINT.dbo.Depot D on M.DepotID = D.DepotID
GROUP BY D.DepotName
"@
            $total = Invoke-Sqlcmd2 -ServerInstance SQL-SERVER -Database COMPLAINT -Query $qtotals -Username username -Password password
            $total | select-object Total, DepotName | Out-UDChartData -LabelProperty "DepotName" -DataProperty "Total" -Dataset @(
            New-UDChartDataset -DataProperty "Total" -Label "Complaints Recorded By Depot" -BackgroundColor "#ccc" -BorderColor "#000" -BorderWidth 1)
            } -AutoRefresh -RefreshInterval 15
```

This will display a nice bar chart of how many complaints each depot has raised.

## Conclusion

Well I smashed this blog tonight, from getting home from work, to taking my laptop to order my chinese take-away to sitting here in total peace and quiet as the rest of my family has gone to bed. Hopefully you have learnt something from this blog, and it helps you out with using powershell universaldashboard.
