# Provision a Hyper Protect Virtual Server

### Prerequisite
* Register for an account at: myibm.ibm.com [:link:](https:myibm.ibm.com)
* Generate or find your SSH public/private RSA key [:link:](https://github.com/IBM-Developer-Puget-Sound/curtain-raiser/blob/master/how_to/ssh/keygen/README.md)
----

1. Login to your IBM cloud account [:link:](https://cloud.ibm.com/login)

2. Click on hamburger menu in the upper left corner.

3. Click on dropdown item `Classic Infrastructure` .

4. Click on the button `Order Devices +` on right hand side.

5. Click on the Services `Compute` category on the left to
   filter the choices.

6. Select the `Hyper Protect Virtual Server` option.

7. Choose the desired pricing plan for the necessary service.
   * Free if you only need a minimal short term device.

8. Choose a memorable `Service Name` related to your project.
   * For example contains the name of
     * the IBM service plus
     * Name of your project
       * `Hyper Protect Virtual Server-myproject-dev`

9. Scroll down the page to enter your `SSH public key`.
   * To allow access the virtual server later.
   * This is the key you found or generated in a previous step on your pc at `~/.ssh/id_rsa.pub` .

10. Click on the `Create` button, on the bottom right of the screen.

11. Expect to wait a while for the service to be generated.
    * The screen will be redirected to your `Resource List`
    * Scroll down to and click on the  `Services` heading to see the Hyper Protect service-name that you just created.
    * Refresh your screen until is shows Status `Active` .

----

12.  Once the Status is `Active`
     * click on the name of your service to bring up a management window.

13.  Scroll down to the very bottom of the page and then click on the `How to connect` button.

14.  See something like:
     * `ssh root@nnn.nn.nn.nn`

15.  Copy and paste the command from the how to connect modal into your command line.
     > note: the IBM screen provides your correct IP numbers, (not the nnn placeholders above)

     * you might need that top secret passphrase here!

### Troubleshooting

* error message: `sign_and_send_pubkey: signing failed: agent refused operation` .

  * did the private key permissions get correct modification?
    * `chmod 600 ~/.ssh/id_rsa`

  * are both public and private keys locally available?
    ```bash
    ls ~/.ssh # returns both
    id_rsa  id_rsa.pub 
    ```

  * do the local and remote fingerprints match?
    ```bash
    ssh-keygen -lf ~/.ssh/id_rsa.pub
    ```
    * see the submitted fingerprint in the management screeen.

----

Reference: 
* cloud . IBM . com docs Hyper Protect virtual server.
  * getting started [:link:](https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-getting-started)

* Youtube
  * IBM developer Puget Sound [:link:]()
  * DTE how to [:link:](https://youtu.be/GlP-w-vsPmc)
