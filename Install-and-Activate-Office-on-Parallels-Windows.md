## Install and Activate Office on Parallels Windows 11

# Installation

1. Download the Office Deployment Tools:

    [https://support.microsoft.com/es-es/topic/office-deployment-tool-9fbd53e3-18a3-1aef-8cfe-e2eaeeeaaa4c](https://support.microsoft.com/es-es/topic/office-deployment-tool-9fbd53e3-18a3-1aef-8cfe-e2eaeeeaaa4c)

2. Create a folder named 'Office' in C:\

3. Execute the downloaded 'officedeploymenttool_17126-20132.exe' aplication.

4. Select yes in the 'User Account Control' pop up which says '¿Do you want to allow this app to make changes to your device?'

5. Check the option 'Click here to accept the Microsoft Software License Terms'.

6. Click on 'Continue'.

7. Select the recently created folder to extract the files there.

8. Click on 'Accept'.

9. Go to the folder 'C:\Office' in the 'File Explorer'.

10. Open the file 'configuration-Office365-x64.xml'.

11. Replace the following line:

    ```
    <Add OfficeClientEdition="64" Channel="PerpetualVL2019">
    ```

    with:

    ```
    <Add OfficeClientEdition="64" Channel="BetaChannel">
    ```

12. Execute the 'setup.exe' application.

# Activation

1. Follow steps given in the following README to execute the MAS created by Windows Addict:

    [https://github.com/Christihan-LB/MAS](https://github.com/Christihan-LB/MAS)

2. Select the option:

    ```
    [4] Online KMS  ^|  Windows / Office  ^|    180 Days
    ```

3. Press any key to return to the main manu.

4. To watch the status after the activation select the option:

    ```
    [5] Activation Status
    ```

5. To exit the program select the option:

    ```
    [0] Exit
    ```