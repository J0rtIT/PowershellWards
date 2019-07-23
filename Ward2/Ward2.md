# Ward2 Variables

Powershell is a powerful tool that is based on the capabilities of one or several Cmdlets to do a specific task. When you associate this Cmdlets, finally you got a script, and this is the whole way of this ward, know the variables and some more cmdlets that can make your life lighter. 

 

Another important fact of the Power of PowerShell is that you can extend his capabilities with programming. Each cmdlet is on the charge of a single action, and when you associate several cmdlets, it allows you to do incredible things. Incredible complicate tasks and even updates into an SQL Server Database hosted on Azure with the single run of a script. 

 

This is precisely the same on the batch scripting on DOS, where you execute a simple commons, and then you associate several commands to do more complicated tasks. That's the beauty of PowerShell, you can combine cmdlets and variables in their different scopes and do amazing things. 

 

Also, there are two kinds of declarations variables (implicit and explicit) and another two ways to declare them, depending if you want to be local to the script or function, or globally all across all scripts and functions. I'll explain this in details ahead. 

## Implicit Variables
You can define variables using implicit methods (like javascript) or tell them the type using the [type] prefix. 

 

In this section, I'll share with you a simple way to define and to get the types of variables. 

 

 

To define a variable implicitly you have to set it to a value, the variable will adapt to the amount you gave, and you define any variable using the char "$" at the start of the name  (ex: $name) 

 

Now let's define and assign a couple of implicit variables and find out what types are designated by the PowerShell console: 

 

$var1 = "this is a string" 

$var2 = 64 

 

Now to get the types, we're gonna use the "Get-Member" Cmdlets. 


  
 ![Get-Member 1](../Images/W2/ward2-1.png)

 ![Get-Member 2](../Images/W2/ward2-2.png)

## Explicit Variables

Also there's a way to do it explicitely if you use the type between [] before the declaration of the variable. 

 

Ex 
 ![Explicit Example 1](../Images/W2/ward2-3.png)

 ![Explicit example 1 more](../Images/W2/ward2-4.png)

## Environmental Variables

Following the analogy with DOS, where you have environment variables like "UserProfile" or "windir" you already have this on PowerShell, so how to get all the variables in your computer? 

 

**Get-ChildItem $Env:<var>**


Alternatively, 

**Gci $env:<var>** 

 

Task: What do you think gci is? Moreover, why it works just like Get-childItem cmdlet? 

 

You use these variables like any other: 

 

**$env:userprofile**

Get the user path of the current logged user where lies all the profile (Documents, Images,etc.) 

 

**$env:tmp**

Get the path of the default Tmp folder (yes, that one that is filled when you download whatever and "run" it from the links without actually saving it into the computer, they go into this path. 

 

**$env:OS** 

The version of the OS (is it NT or not). 

 

**$env:AppData**

The path of the Application data folder for the current user. 

 

 

Some uses: 

 

**$> Cd $env:userprofile**

Navigate into the current user profile path 

 

**$> Get-Process | Convertto-Html | out-file $env:tmp/file.html**

Get a list of all the processes on the current computer, convert the objects into Html and then export them into a file called: file.html in the $env:tmp folder 

## Global Variables

Sometimes while doing a script, it's required that the variables values or pointers are preserved over the run of several functions or processes. For these individual variables, we use the "$GLOBAL:" prefix followed by the name of the variable. 

 

Like on regular C programming, we have local variables and global variables the local variables are local to the current function, and it's destroyed once the function where it belongs ends. In other had the global variables are considered global to the session, this means that they will preserve its value even when the script finishes if it's not removed correctly, which can lead to security issues if they're not being taken with conscience. 
 

> [!IMPORTANT]
> All variables are not Case Sensitive 



 Let's suppose we have an script: 

 <#
#### 

$Global:testpath = $env:userprofile 

 

Write-Host "the value of the variable Global:Testpath is $global:testpath - Before function" 

 

#function definition 

Function testfund{ 

 $global:testpath="new value 1234" 

} 

 

#what would be the value of this line?, test it on (Powershell ISE), copy and paste it 

Write-Host "the value of the variable Global:Testpath is $global:testpath - Before function" 

#### 
#>

<#
#### 

$Global:testpath = $env:userprofile 

 

Write-Host "the value of the variable Global:Testpath is $global:testpath - Before function" 

 

#function definition 

Function testfund{ 

 $global:testpath="new value 1234" 

} 

 

Testfund() 

 

#what would be the value of this line?, test it on (Powershell ISE), copy and paste it 

Write-Host "the value of the variable Global:Testpath is $global:testpath - Before function" 

#### 
#>

 Compare both and tell me your thoughts


## Local Variables

There are variables that you just need to do a specific task and then you'd like to be destroyed. 

 

One typical example is any variable that we define like this  

$var1 = "test" 

 

This $var1 is local to the session where we are working on and it will be there until we remove it manually (next section) 

## Cleaning Up Variables
If the variables are global you'd need to do the clean up  

 

### Global Variables 

#definition $global:ThisIsAnExample="Example" 

Remove-variable -global ThisIsAnExample  
 

There is no typo, you do not add the $ while removing variables, and add -global parameter for global variables 

 
### Local Variables 

#definition $ThisIsAnExample="Example" 

Remove-variable ThisIsAnExample  

 

Without "$" and with the -global parameter 

 

There is no typo, you dont add the $ while removing variables. 


# Cmdlets on this ward

The documentation on these cmdlets can be searched here: 


 [Get-Member](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-member?view=powershell-6) 

 [Get-ChildItem](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Management/Get-ChildItem?view=powershell-6)

 [Remove-variable](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/remove-variable?view=powershell-6)




