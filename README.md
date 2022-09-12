<p>You have to act as an in-game character in the GTA Online-Samp server.  When you enter the game, you must have a license to drive a car, which you can get by taking a test.  In this server you can work, earn money and play.  Buy a house, car, etc. for yourself.  If you do something wrong, the police will deal with you and...

So stay with us until the end of this article from Azardita's blog to teach you how to build a GTA San Andreas game server or the SAMP server.

Once the files are downloaded, you should extract the zip file anywhere you like;  After extracting the above zip file, you should see the following files inside it:

         » server.cfg (file)

         » server-readme.txt (file)

         » samp-server.exe (file)

         » samp-licence.txt (file)

         » announce.exe (file)

         » scriptfiles (folder)

         » spawno (folder)

         » gamemodes (folder)

         » filterscripts (folder)
 
For example, we use lvdm.pwn mode in this tutorial;  But if you have scripting knowledge, you can make your mod.

Go to the gamemodes folder to find the lvdm.pwn file.

When you open the server.cfg file, you will see an environment similar to the following image:

* Change the rcon_password changeme line to the password you like.

* announce 1 means whether the server will be announced in the list of SA-MP servers (1) or not (0), which you can private or make public.

* filterscripts is for specifying filters in the game process on the server.

* anticheat should be set to 0 (if set to 1) it may crash your server.

## Adding a vehicle in the samp server

If you intend to add a vehicle to the Samp game server, you must first know where the cars and engines should appear.  For this, first you need to run the samp_debug.exe file and then click on the "Launch Debug" button.

Use /v <modelid> to create your desired vehicle and then save it with /save <nameyouchoose>.
Then enter your GTA game folder and open the savedpositions.txt file.  After opening this file, you will see the following code:
</p>
