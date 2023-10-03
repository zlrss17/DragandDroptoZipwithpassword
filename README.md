# DragandDroptoZipwithpassword

title Drag, Zip

Setlocal EnableDelayedExpansion
Set _RNDLength=12
Set _Alphanumeric=ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789
Set _Str=%_Alphanumeric%987654321
:_LenLoop
IF NOT "%_Str:~18%"=="" SET _Str=%_Str:~9%& SET /A _Len+=9& GOTO :_LenLoop
SET _tmp=%_Str:~9,1%
SET /A _Len=_Len+_tmp
Set _count=0
SET _RndAlphaNum=
:_loop
Set /a _count+=1
SET _RND=%Random%
Set /A _RND=_RND%%%_Len%
SET _RndAlphaNum=!_RndAlphaNum!!_Alphanumeric:~%_RND%,1!
If !_count! lss %_RNDLength% goto _loop
echo !_RndAlphaNum! > "Zip file password is "!_RndAlphaNum!
echo !_RndAlphaNum!|clip
7z a -tzip "%~1.zip" "%~1" -p!_RndAlphaNum!
echo :)
echo Completed!
echo Press any key to exit.
pause >nul
exit
