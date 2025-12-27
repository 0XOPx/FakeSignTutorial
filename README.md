# Step 1: Open PowerShell as Administrator
# (Right-click Start → Windows PowerShell (Admin) or Terminal (Admin))

# Step 2: Create folder and certificate
New-Item -Path "C:\Cert" -ItemType Directory -Force

$cert = New-SelfSignedCertificate -Type CodeSigningCert `
    -Subject "CN=OXOP" `
    -KeyAlgorithm RSA `
    -KeyLength 2048 `
    -HashAlgorithm SHA256 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -NotAfter (Get-Date).AddYears(10)

Export-PfxCertificate -Cert $cert `
    -FilePath "C:\Cert\OXOP.pfx" `
    -Password (ConvertTo-SecureString -String "OXOP" -Force -AsPlainText)

Export-Certificate -Cert $cert -FilePath "C:\Cert\OXOP.cer"
# Trust the Certificate (so it shows "Verified publisher")

1. Double-click `C:\Cert\OXOP.cer`
2. Click **Install Certificate**
3. Select **Local Machine** → Next
4. Choose **Place all certificates in the following store**
5. Browse → **Trusted People** → OK → Next → Finish
6. Click **Yes** on the security warning
# Sign your EXE (run in admin Command Prompt)
"C:\Program Files (x86)\Windows Kits\10\bin\10.0.22621.0\x64\signtool.exe" sign ^
    /f "C:\Cert\OXOP.pfx" ^
    /p OXOP ^
    /tr http://timestamp.acs.microsoft.com ^
    /td SHA256 ^
    /fd SHA256 ^
    /v "C:\Path\To\YourApp.exe"
# Distribute
- Share the signed EXE + all required files.
- On other machines: signature shows your name in details.
- To show "Verified publisher" there too: give them the `.cer` file and have them install it to **Trusted People** (same steps above).


Send [this](https://github.com/0XOPx/FakeSignTutorial/blob/main/send-this-to-repos/GUIDE%20ON%20MAKING%20IT%20SIGNED.md) btw.
