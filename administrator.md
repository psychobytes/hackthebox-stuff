# HackTheBox - Administrator
- Difficulty : Medium
- Category : Windows

1. scan open port & running service using nmap. (ftp, smb, ldap (active directory), rpc are running.)
   
   ![image](https://github.com/user-attachments/assets/f6150363-2322-4dd1-859b-d7beaed66720)


2. try to login via ftp. (failed).
   
   ![image](https://github.com/user-attachments/assets/5573f8a3-4055-4a94-b233-d595baf09b17)


3. use enum4linux to enumerate shares, user, etc. dont forget to enumerate using the provided creds.

   ![image](https://github.com/user-attachments/assets/d98ca7c4-234e-424a-baf1-e3aa0493656a)


4. enumerate read access to shares using netexec. (no read access to machine)

   ![image](https://github.com/user-attachments/assets/ac6dd418-65f5-4399-8844-c069cca7d88f)


5. enumerate AD using bloodhound.
   
   ![image](https://github.com/user-attachments/assets/72b1602a-112c-4039-897d-7ccc5099a171)


6. start from our default user, check what we own and what we can do. Olivia (our default user) has genericall privilege to michael, we can change michael password.
   
   ![image](https://github.com/user-attachments/assets/598d0007-68b0-4d2a-81a9-9b1bbb656b3a)

   change michael password

   ![image](https://github.com/user-attachments/assets/4b71fca2-9d07-4d00-9228-61721a6280d7)
   

8. try login as michael

   ![image](https://github.com/user-attachments/assets/90cb5c11-45dd-4087-986b-6a07f0f6958e)
   

9. back to bloodhound, check what michael can do. michael have forcechangepassword privilege to benjamin user
   
   ![image](https://github.com/user-attachments/assets/99fbf291-69b8-4dc4-a26e-d79d78173467)
   

10. change benjamin password and test login via smb
    
    ![image](https://github.com/user-attachments/assets/8507eb7a-a7ca-488a-ba83-2ef417d72975)
    

11. remember the ftp that we found while scanning using nmap in the first step ? try using that now.
    
    ![image](https://github.com/user-attachments/assets/5dc93d30-6534-4fcf-8705-58b31fd4b032)

12. download Backup.psafe3 from ftp.
    
    ![image](https://github.com/user-attachments/assets/ce06746d-3c0c-4f80-9253-67c000213146)

13. what is .psafe3 file ? google it, its a passwordsafe database file. passwordsafe is password manager and that file is containing password.
    
    ![image](https://github.com/user-attachments/assets/24cd427f-125d-4150-8de7-9422ea5f4712)

14. crack the file using hashcat.

    ![image](https://github.com/user-attachments/assets/42cbbe7c-654e-427d-baa8-f2c73c9eabf5)
    ![image](https://github.com/user-attachments/assets/fabe6c60-544c-41a5-ae8f-534def586eb5)

15. open Backup.psafe3 file using Password Safe software (download here : https://pwsafe.org/). use the password that cracked earlier.

    ![image](https://github.com/user-attachments/assets/2d42a449-3a38-4de9-aa9d-e32f3fe4b6e0)
    ![image](https://github.com/user-attachments/assets/e06d75d3-6182-4297-8a98-2bfb01a9f3b0)

16. login as emily and grab user flag

    ![image](https://github.com/user-attachments/assets/889158a0-299f-4ebf-985b-5288a4553dbd)
    ![image](https://github.com/user-attachments/assets/e2bd5e45-053d-4616-a922-23f2b2867f7a)


18. back to bloodhound, check what emily can do.
    
    ![image](https://github.com/user-attachments/assets/bbf27222-d42f-4b41-aaec-53c36495c971)

19. 
