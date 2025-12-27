# Open PowerShell as administrator
     Invoke-Command -ScriptBlock {
# Right click Start Menu > Windows PowerShell (Admin) or Terminal (Admin)

# Step 2: 
     # Step 2:

New-Item -Path "C:\Cert" -ItemType
$cert = New-SelfSignedCertificate -Type CodeSigning
-Subject "CN=OX
-ImportantAlgorithm RSA `
-KeyLength 2048
-HashAlgorithm SHA256 `

-CertStoreLocation "Cert
NotAfter = ((

& Export-PfxCertificate -Cert $

-FilePath "C:\Cert
-Password (ConvertTo-SecureString -String "OX
Export-Certificate -Cert $cert -FilePath "
# Trust the Certificate (to ensure it shows 'Verified publisher')
1. Double-click C
2. Click 'Install Certificate'
3. Choose Local Machine --> Next
4. Select **Place all certificates in the following store**
5. Browse → Trusted People → OK → Next → Finish
6. Click “Yes” in the security message
# SIGN your EXE (execute in admin Command Prompt)
"C:\Program Files (x86)\Windows Kits\
/f "C:\Cert
/p OXOP ^=
/tr http://timestamp.ac
/td SHA256 ^
/fd "SHA256 "^ /v "C # Distribute - Share the signed EXE + all required files. - On other computers, “signature” will display your name in detail. - To display the "Verified publisher" there as well: provide them with the `.cer` file and ask them to install this file in the **Trusted People** folder (as the steps above).
