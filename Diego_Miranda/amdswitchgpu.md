AMD igpu dgpu hybrid handling needed the switcheero package and activate it basically..

And some xrandr commands

Switcheroo-control:

```
aur/switcheroo-control-git 2.3.r6.g9bcb7b5-1 (+0 0.00) 
    D-Bus service to check the availability of dual-GPU
aur/switcheroo-control 2.5-3 (+38 2.96) 
    D-Bus service to check the availability of dual-GPU
```
    
    
https://gitlab.freedesktop.org/hadess/switcheroo-control

`sudo systemctl enable --now switcheroo-control.service`


`Xrandr --lisproviders`

`Xrandr --provideroffloadsink (id of dgpu) (id of igpu )`
