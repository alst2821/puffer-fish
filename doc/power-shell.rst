
============

.. _Get-ChildItem:  https://go.microsoft.com/fwlink/?LinkID=113308
.. _Get-Command: https://go.microsoft.com/fwlink/?LinkID=113309
.. _Get-Help: https://go.microsoft.com/fwlink/?LinkID=113316
.. _Get-Member: https://go.microsoft.com/fwlink/?LinkID=113322
.. _Get-Module: https://go.microsoft.com/fwlink/?LinkID=141552
.. _Select-Object: https://go.microsoft.com/fwlink/?LinkID=113387
.. _Sort-Object: https://go.microsoft.com/fwlink/?LinkID=113403
.. _Group-Object: https://go.microsoft.com/fwlink/?LinkID=113338
.. _Where-Object: https://go.microsoft.com/fwlink/?LinkID=113423
.. _`Comparison operators`: https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-6
.. _Start-Service: https://go.microsoft.com/fwlink/?LinkID=113406
.. _Foreach-Object: https://go.microsoft.com/fwlink/?LinkID=113300

Instructor is Jeff Hicks in pluralsight.

There's online help for commands and on the command line
e.g:

* Get-ChildItem_
* Get-Command_
* Get-Help_
* Get-Member_
* Get-Module_
* Group-Object_
* Select-Object_
* Sort-Object_
* Where-Object_
* `Comparison operators`_
  
The links were obtained by asking Get-Help_ that lists a shortened URL
at "go.microsoft.com". All links are in the hierarchy of
`'PowerShell Documentation' <https://docs.microsoft.com/en-gb/powershell/?view=powershell-6>`_.
  

Example commands
----------------
::

   $psversiontable

   Get-PSSnapin

   Get-PSSnapin -Registered

   Get-Command -Module <modulename>

   Get-Command -Module Microsoft.PowerShell.Management

   Get-Module -ListAvailable

A very long list of properties of module objects::

  Get-Module | Select-Object * | more


  import-module

  dir $pshome
  $pshomemodules

  $env:psmodulepath -split ";"

  import-module storage

  remove-module storage

PowerShellGet::
  
  get-command -module PowerShellGet | more

  Get-PSRepository

  find-module -tag sqlserver

  find-module sqlserver | select-object *

  powershell-get

  save-module sqlhelper -path c:\save

  dir c:\save -recurse | more

  ise c:\save\sqlhelper\1.1\sqlhelper.psm1

  install-module <name> -scope CurrentUser

  get-command -noun Module


Examples with the psteachingtools module
----------------------------------------

Examples::
  
  Get-Vegetable | Get-Member -Membertype Method

  Get-Vegetable | Get-Member -Membertype Property

Examples of the Select-Object_ cmdlet::

  Get-Vegetable | Select -property Name

  Get-Vegetable | Select Name,Count,State

  Get-Vegetable | Get-Member

  Get-Vegetable | Select Name,Count,CookedState,IsRoot

  Get-Vegetable | Select Name, C*

Select a number of objects::

  Get-Vegetable | Select -First 1

Discovering the propery names by other method (handy technique)::

  Get-Vegetable | Select -First 1 -Property *

  Get-Vegetable | Select Name -Unique

Example below to generate a list to export to a text file, for example::
  
  Get-Vegetable | select -unique -expandproperty name
    
Examples of the Sort-Object_ cmdlet::

  Get-Vegetable | Sort Count

  Get-Vegetable | Sort Count -Descending

  Get-Vegetable | Sort Count -Descending | Select Count,Name

  Get-Vegetable | Sort color -unique

Advanced stuff::

  Get-Vegetable | Select Name,Color,@{Name="ColorValue";Expression={$_.color.value__}} | sort Color

  Get-Vegetable | sort {$_.color.tostring()} -Unique
  
Explanation: the color property is an enumeration in reality and under the hood
it uses an integer.
k

Examples using the Group-Object_ cmdlet::

   Get-Vegetable | Group-Object -Property Color

   Get-Vegetable | Group Color | sort count -Descending

   Get-Vegetable | Group Color | sort count -Descending | select -first 1 -expandproperty group

   Get-Vegetable | Group CookedState -NoElement

Examples using the Where-Object_ cmdlet::

  Get-Vegetable | where-object -property color -eq yellow

  Get-Vegetable | where {$_.color -eq 'yellow' }

  Get-Vegetable | where {$psitem.color -eq 'yellow'}

The comparisons use comparison operators, documented `here <https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-6>`_ and here's examples::

  1 -eq 1
  True
  
  1 -lt 5
  True

  1 -gt 5
  False

  'power' -eq 'Power'
  True

  'power' -ceq 'Power'
  False

  'outlookconnector' -like 'outlook*'
  
  'outlookconnector' -notlike 'outlook*'

   'outlookconnector' -match '^Ou'

   'serv442' -match '\w+\d{1,3}'

  
Filtering using the comparison operators::

  Get-Vegetables | where {$_.isRoot -OR $_.color -eq 'green'}

  Get-Vegetables | where {$_.isRoot -eq $False }

  Get-Vegetables | where {-not ($_.isRoot)} | select name, isRoot

  
Testing the speed::

  Measure-Command {dir c:\windows\System32 -recurse | where { $_.Extension -eq '.exe'}}
  
  Measure-Command {dir c:\windows\System32 -recurse -filter *.exe }


Advanced examples (using Start-Service_)::

  get-eventlog system | group source -noelement | sort count -Descending | select -first 10 | out-gridview

  get-service bits | select *

  get-service | where status -eq 'stopped'

  get-service | where status -eq 'stopped' | select displayname, name,starttype

  get-service | where {$_.status -ne 'running' -and $_.starttype -eq 'automatic'}

  get-service | where {$_.status -ne 'running' -and $_.starttype -eq 'automatic'} | start-service -passThru

  $s = Get-Service wmi
  Start-Service -InputObject $s -PassThru | Format-List >> services.txt

  
Pipeline exceptions
-------------------

To do something to an individual object.
This uses Foreach-Object_::
  



