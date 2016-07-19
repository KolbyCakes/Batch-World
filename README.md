# Batch-World
save as a .bat or .cmd file
Have Fun!!!
------------CODE\/-------------
@echo off
title Game 175
setlocal enabledelayedexpansion

::=====================GAME=INTERFACE===================

:menu
cls
color 0a
echo                                          ÛÛÛÛÛ   ÛÛÛ  ÛÛÛÛÛ ÛÛÛÛÛ Û    Û 
echo                                          Û    Û Û   Û   Û   Û     Û    Û
echo                                          ÛÛÛÛÛ  ÛÛÛÛÛ   Û   Û     ÛÛÛÛÛÛ
echo                                          Û    Û Û   Û   Û   Û     Û    Û
echo                                          ÛÛÛÛÛ  Û   Û   Û   ÛÛÛÛÛ Û    Û
echo.
echo                                          Û       Û ÛÛ  ÛÛÛÛ  Û    ÛÛÛ
echo                                           Û     Û Û  Û Û  Û  Û    Û  Û
echo                                            Û Û Û  Û  Û ÛÛÛÛ  Û    Û  Û
echo                                             Û Û    ÛÛ  Û   Û ÛÛÛÛ ÛÛÛ
echo.
echo                                              1)Create New Character
echo                                                    2)Continue
echo                                                    3)Options
echo                                                    4)Credits
echo                                                     5)Quit
echo.
set /p c=Enter:
if !c! == 1 goto CharNew
if !c! == 2 goto CharLoad
if !c! == 3 goto Options
if !c! == 4 goto StreetCred
if !c! == 5 exit
goto menu
:CharNew
cls
set /p name=Please enter a username for your new character:
set health=50
set armor=0
set CurWpn=Fists
set wpnDmg=1
set money=0
goto GameMenu



:CharLoad
cls
set /p name=Enter Name:
for /f %%a in (BW_!name!.sav) do set %%armor
goto GameMenu

:Options
cls
echo Error
pause >nul
goto menu
:StreetCred
cls
echo Idea: Jokim Skar
echo Programmer: Kolby Klecz
pause>nul
goto Menu
:GameMenu
cls
echo Name: !name!
echo Weapon: !CurWpn!
echo.
echo Health: !health!
echo Armor: !armor!
echo.
echo 1)Attack some guy
echo 2)Exit
echo.
set /p c=Enter:
if !c! == 1 goto AttackSome
if !c! == 2 exit
goto GameMenu

::=====================COMBAT===================

:AttackSomeNew
set /a Enemy_Name=Guy1
goto AttackSome
:AttackSome
cls
echo !Enemy_Name!: !!
echo You: !health!
echo.
echo 1)Attack
echo 2)Save
echo 3)RUN!
echo.
set /p c=Enter:
if !c! == 1 goto Attack
if !c! == 2 goto SaveGame
if !c! == 3 goto GameMenu
goto AttackSome

:Attack
set /a !Enemy_Name!_HP-=!wpnDmg! 
set /a health-=!%Enemy_Name%_Attack!
if !%EnemyName%_HP! LSS 1 goto win
if !health! LSS 1 goto YouSuck
goto AttackSome

:win
cls
echo YOU WIN!
echo.
pause >nul
goto GameMenu
:YouSuck
cls
echo YOU SUCK!
echo.
pause >nul
goto GameMenu

::=====================ENEMIES=======================

:Guy1
set Guy1_HP=10
set Guy1_Attack=1
goto AttackSome
::=====================CORE=FUNCTION===================

:SaveGame
cls
echo Saving...
(echo name=!name!)>>BW_!name!.sav
(echo health=!health!)>>BW_!name!.sav
(echo armor=!armor!)>>BW_!name!.sav
(echo CurWpn=!CurWpn!)>>BW_!name!.sav
(echo wpnDmg=!wpnDmg!)>>BW_!name!.sav
(echo money=!money!)>>BW_!name!.sav
goto GameMenu
:exit
cls
echo Are you sure? [Y,N]
echo.
set /p c=Enter:
if !c! == y exit
if !c! == n goto menu
if !c! == Y exit
if !c! == N goto menu
