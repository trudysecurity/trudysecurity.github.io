---
published: true
---

![1-1.png]({{site.baseurl}}/htb/spectra/1-1.png)








###  Let's add spectra to our host file and check for open ports




![1-2.png]({{site.baseurl}}/htb/spectra/1-2.png)





### Let's take a closer look at port 80
### Hello Jira






![1-1.png]({{site.baseurl}}/htb/spectra/1-3.png)




### Below we see they are running WordPress





![1-1.png]({{site.baseurl}}/htb/spectra/1-4.png)





### Test link





![1-1.png]({{site.baseurl}}/htb/spectra/1-5.png)





### Removing the `index.php` from the URL give us 





![1-1.png]({{site.baseurl}}/htb/spectra/1-6.png)





### Viewing `wp-config.php.save` loads a blank screen





![1-1.png]({{site.baseurl}}/htb/spectra/1-7.png)





### However, viewing the source of the page reveals credentials





![1-1.png]({{site.baseurl}}/htb/spectra/1-8.png)





### Dirbuster time





![1-1.png]({{site.baseurl}}/htb/spectra/1-9.png)





### Brute forcing the directories we get the following





![1-1.png]({{site.baseurl}}/htb/spectra/1-10.png)





### `main/index.php` leads us to our login portal





![1-1.png]({{site.baseurl}}/htb/spectra/1-11.png)





### `dev and devtest` don't work as a username






### Wordpress default credential for admin is administrator






### `administrator:devteam01` gets us a foothold






![1-1.png]({{site.baseurl}}/htb/spectra/1-12.png)





### Let's open up msfconsole






### Theres a module called `wp_admin` that can be used when you have admin credentials on a wordpress site. 





![1-1.png]({{site.baseurl}}/htb/spectra/1-13.png)






![1-1.png]({{site.baseurl}}/htb/spectra/1-14.png)





### Next I populate the info 






![1-1.png]({{site.baseurl}}/htb/spectra/1-15.png)






### And we get our meterpreter







![1-1.png]({{site.baseurl}}/htb/spectra/1-16.png)






![1-1.png]({{site.baseurl}}/htb/spectra/1-17.png)





### There is some functionality





![1-1.png]({{site.baseurl}}/htb/spectra/1-18.png)






![1-1.png]({{site.baseurl}}/htb/spectra/1-19.png)





### `cat /etc/passwd` we find user `katie`





![1-1.png]({{site.baseurl}}/htb/spectra/1-20.png)






### Looking for a name file passwd







### `find / -name *passwd* 2>/dev/null` 






![1-1.png]({{site.baseurl}}/htb/spectra/1-21.png)






### inside of the `/etc/autologin/passwd` we find 






![1-1.png]({{site.baseurl}}/htb/spectra/1-22.png)






### We can now ssh into the system with the credentials `katie:SummerHereWeCome!!`






![1-1.png]({{site.baseurl}}/htb/spectra/1-23.png)






![1-1.png]({{site.baseurl}}/htb/spectra/1-24.png)





### And we get the user flag!






![1-1.png]({{site.baseurl}}/htb/spectra/1-25.png)






### Time for priv esc





### Checking permissions


![1-1.png]({{site.baseurl}}/htb/spectra/8b8ad00afd3144aeb74e10f990a32d1a.png)

`find / -group developers -ls 2>/dev/null`

![1-1.png]({{site.baseurl}}/htb/spectra/c711201e42e1434399b7494b9a0b1981.png)

### test.conf is owned by root but we have write permissions as katie is in the developers group


![1-1.png]({{site.baseurl}}/htb/spectra/4c8338e9d8374a249c147953af0721f4.png)

### Let's edit the above script


![1-1.png]({{site.baseurl}}/htb/spectra/10cad3a3a4de4329b11740c5bb6bc25f.png)

`sudo /sbin/initctl start test`


![1-1.png]({{site.baseurl}}/htb/spectra/94173dd8c9bf448a9557ce30866b9af6.png)

### We have to be quick or the test.conf file will be overwritten

`/bin/bash -p`


![1-1.png]({{site.baseurl}}/htb/spectra/6b8c3d2259f14de1adb5d6f7dc59f314.png)

### Below we get our root flag!


![1-1.png]({{site.baseurl}}/htb/spectra/362921d9c00a4aa08854cd87984f530c.png)

### Machine Owned







































