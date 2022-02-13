

# Please read the all documentation if this doc is not working. documentation linked below step by step

https://pub.dev/packages/msix

## package config

### pubspec.yaml
#### msix_config:
####   publisher: CN=Blackshadow
####   display_name: Blackshadow
####   publisher_display_name: Blackshadow
####   identity_name: MyCompany.MySuite.MyApp
####   msix_version: 1.0.0.0
####   logo_path: G:\Windows-Installer-with-NSIX-and-Certificate\assets\utils\logo.png
####   certificate_path: G:\Windows-Installer-with-NSIX-and-Certificate\assets\utils\cert.pfx
####   certificate_password: 1234

## First step
 <div class="row"> 
   <img src="screenShots/s1.png" alt="Screenshot 1" width="400" height="200"> 
 </div> 
 
### https://docs.microsoft.com/en-us/windows/msix/package/create-certificate-package-signing

### PowerShell

New-SelfSignedCertificate -Type Custom -Subject "CN=Contoso Software, O=Contoso Corporation, C=US" -KeyUsage DigitalSignature -FriendlyName "Your friendly name goes here" -CertStoreLocation "Cert:\CurrentUser\My" -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.3", "2.5.29.19={text}")
 <div class="row"> 
   <img src="screenShots/s2.png" alt="Screenshot 1" width="800" height="400"> 
 </div>
 
### PowerShell

Set-Location Cert:\CurrentUser\My
Get-ChildItem | Format-Table Subject, FriendlyName, Thumbprint

 <div class="row"> 
   <img src="screenShots/s3.png" alt="Screenshot 1" width="800" height="250"> 
 </div>
 
### predefined certificate path
G:\Windows-Installer-with-NSIX-and-Certificate\assets\utils\cert.pfx
### Thumbprint
4E846D68B6C60EB6B86D5DEFF34EC3739AA03508

### Export a certificate. Password usage
### doc
$password = ConvertTo-SecureString -String <Your Password> -Force -AsPlainText 
Export-PfxCertificate -cert "Cert:\CurrentUser\My\<Certificate Thumbprint>" -FilePath <FilePath>.pfx -Password $password

### ready to run
$password = ConvertTo-SecureString -String 1234 -Force -AsPlainText 
Export-PfxCertificate -cert "Cert:\CurrentUser\My\4E846D68B6C60EB6B86D5DEFF34EC3739AA03508" -FilePath G:\Windows-Installer-with-NSIX-and-Certificate\assets\utils\cert.pfx -Password $password

<div class="row"> 
   <img src="screenShots/s3.1.png" alt="Screenshot 1" width="800" height="350"> 
</div>

## Second step
https://community.flexera.com/t5/InstallShield-Knowledge-Base/How-to-add-certificates-to-the-Trusted-Root-Certification/ta-p/4118

#### 1. Click Start, click Start Search, type mmc, and then press ENTER.
 
 <div class="row"> 
   <img src="screenShots/s4.png" alt="Screenshot 1" width="450" height="300"> 
 </div>
 
#### 2. On the File menu, click Add/Remove Snap-in.
  
<div class="row"> 
   <img src="screenShots/s5.png" alt="Screenshot 1" width="650" height="350"> 
</div>
   
#### 3. Under Available snap-ins, click Certificates,and then click Add. 
#### 4. Under This snap-in will always manage certificates for, click Computer account, and then click Next.
#### 5. Click Local computer, and click Finish.
#### 6. If you have no more snap-ins to add to the console, click OK.
#### 7. In the console tree, double-click Certificates (Local Computer). double-click Certificates.
#### 8. Right-click the Trusted Root Certification Authorities store - select All Tasks.
#### 9. Click Import to import the certificates and follow the steps in the Certificate Import Wizard.
  
<div class="row"> 
   <img src="screenShots/s6.png" alt="Screenshot 1" width="700" height="350"> 
</div>
  
#### 10 Browse and navigate to the .pfx file. and next
  
<div class="row"> 
   <img src="screenShots/s7.png" alt="Screenshot 1" width="700" height="500"> 
</div>
    
#### 11 Password 1234 and next => next => Finish => OK
  
<div class="row"> 
   <img src="screenShots/s8.png" alt="Screenshot 1" width="500" height="250"> 
   <img src="screenShots/s9.png" alt="Screenshot 1" width="280" height="160"> 
</div>  
   

## Third step
#### flutter clean
#### flutter build windows --release
#### flutter pub run msix:create
### msix created: build\windows\runner\Release\windows_installer_msix_dertificate.msix




