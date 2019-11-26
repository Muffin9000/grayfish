# check starts as False (failed)
$check = $False
$errorCheck = $False
$errText = ""
$crayfishServiceLog ='D:\WS_Crayfish\Tele2_NL_WS_WLR_Live\errorlogs\logDebug.txt'
#'D:\grayfish\testlog.txt'
$logFile = 'D:\grayfish\errorLog.rtf'
$logMaxLines = 5000
$crayDiplyaName = 'WLRService'
$currDate = Get-Date -Format "dd/MM/yyyy HH:mm K"


# fuction that restarts the service given in the parameter funtionName -servineName "ServiceDisplayName"
function rstService {

    Param(
            [string]$serviceName,
            [switch]$otherStream
    )

    # get the service and restart it
    $service = Get-Service -DisplayName $serviceName
    $service | Restart-Service

    # if running then restart was successful
    if ($service.Status -eq "Running"){
        Write-Host "$serviceName Restarted"
        "$serviceName Restarted" | Out-File -filepath $script:logFile -Appen

        if($otherStream){
            "$serviceName Restarted on $script:currDate due to: `n"
        }
    } Else {
        # if not service still not running restart again
        Write-Host "$serviceName Is not running. Attempting to Start Service Again..."
        $service | Start-Service

        if($otherStream){
            "$serviceName Is not running. Attempting to Start Service Again... $script:currDate `n"
        }

        if($service.Status -eq "Running"){
            Write-Host "$serviceName Restarted"

            if($otherStream){
                "$serviceName Restarted $script:currDate `n"
            }
        }Else{
            Write-Host "$serviceName Did not Start please start Manually"

            if($otherStream){
                "$serviceName Did not Start please start Manually $script:currDate `n"
            }
        }
    }
}


# get last 12 line from CrayFish service log files (path defined above)
$str = Get-Content $crayfishServiceLog -Tail 12 | ForEach {

    # add each line to $script
    $script:errText += $_ + "`n"

    # check if there is an error or fatal error
    if(($_ -Match "ERROR") -or ($_ -Match "FATAL")){
        $script:errorCheck = $True

    }


    # if crayfish log has conditions below put $check as True
    if(($_ -like "*this operation is:Open") -or ($_ -like "-Starting process*") -or ($_ -like "*Transfer Windows service*"))  {

            $script:check = $True
    }
}

if($script:errorCheck){
    $script:message = "Error - Status not Open `n "
    Write-Host $message -ForegroundColor Red
    Write-Host $script:errText -ForegroundColor Red 

    rstService -serviceName $crayDiplyaName 
}

Else {
    # check $status true or false
    if(($script:check)){
        # write OK status to concole
        Write-Host "OK - Status OPEN" -ForegroundColor Green
        "OK - Status OPEN" | Out-File -filepath $script:logFile -Append
        # write $script colected lines to errText
        Write-Host $script:errText
    }

    # if check did not pass (False) print the errors form the logDebug.txt and call the restartService function
    Else {
        Write-Host "Error - Status not Open `n "
        "Error - Status not Open `n " | Out-File -filepath $script:logFile -Append
        Write-Host $script:errText  -ForegroundColor Red 

        rstService -serviceName $crayDiplyaName -otherStream | Out-File -filepath $script:logFile -Append
    }
}

# write to log file
$script:errText | Out-File $script:logFile -Append

# if logfile has more than 1000 lines erase 200 lines
$lines = Get-Content $script:logFile | Measure-Object –Line

# if file has more than 5000 lines erase 200 lines
if ($lines.Lines -gt $logMaxLines){
    Get-Content $script:logFile | Select-Object -Skip 200 | Out-File $script:logFile #append function output to logFile
}
