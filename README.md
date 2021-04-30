## Create or modify an ASNA Database Name. 

> Important: This code applies only to DataGate 16.x clients. 

> Important: Any binary created using the `ASNADBName` class must be run with Windows adminstrative rights.

The `ASNADBName` class provides six public methods that you can use to maintain database names programatically with AVR. Add the `ASNADBName` class to your project (or package it in a DLL and reference that DLL in your project) and use the example code below. 

Defaults are set in the `AssignCustomSourceProfileDefaults` method.

|Name               | Default             |
|-------------------|---------------------|
|InitialLibraryList | *No default         |
|Label              | DB2                 |
|PasswordType       | Secure password     |
|PlatformAttribute  | *DATALINK           |
|PoolingTimeout     | 20                  |
|Port               | 5042                |
|Server             | *No default         |
|SSLOptions         | Use SSL if possible |
|SSLCertificateName | *ANY                |

Methods: 

---

##### ResetSourceProfile()

Reset database name attributes back to ASNA defaults. 

---

##### AssignCustomSourceProfileDefaults()

Assign your custom defaults to the database name. Modify this routine as needed.

---

##### CreatePublic(`DBNAME`, `USER`, `PASSWORD`)

Create a public name. Be sure to call either `AssignCustomSourceProfileDefaults` or `ResetSourceProfile` before calling `CreatePublic`. `CreatePublic` overwrites an existing database name. There is no update update method. To update a database name, use `CreatePublic` again.

---

##### CreatePrivate(`DBNAME`, `USER`, `PASSWORD`)

Create a privatec name. Be sure to call either `AssignCustomSourceProfileDefaults` or `ResetSourceProfile` before calling `CreatePrivate`. `CreatePrivate` overwrites an existing database name. There is no update update method. To update a database name, use `CreatePrivate` again.

---

##### Delete(`DBNAME`)

Delete a database name.

---

##### ChangeCredentialse((`DBNAME`, `USER`, `PASSWORD`)

Change the credentials for a database name.

---

Code examples:

    DclFld DBName Type(ASNADBName) New()

    // Be sure to call either `AssignCustomSourceProfileDefaults` or
    // `ResetProfile` before calling the `Create` method.

    // To apply your custom defaults, use this to apply them
    // before calling the `Create` method.
    DBName.AssignCustomSourceProfileDefaults()
    
    // If you don't want to apply custom defaults, call this 
    // method to see the all values to intrinsic defaults.
    DBName.ResetProfile()

    // Assign other values for the database name.
    DBName.SourceProfile.Server = '10.1.3.209'
    DBName.SourceProfile.Port = 5160

    // Optionally override SSL settings.
    // Only connect using SSL; any cryptographically-valid server certificate
    // is accepted, without further validation.
    // DBName.SourceProfile.SslOptions = ASNA.DataGate.Common.SslOptions.Require

    // Optionally set initial library list like this:
    // DGDBName.SourceProfile.InitialLibraryList = *New *String[] {'rpwork', 'dg8_160'}

    // Create a public name.
    DBName.CreatePublic('rpDelete6', 'username', 'password')

    // Create a private name.
    DBName.CreatePrivate('rpDelete6', 'username', 'password')

    // Change user name and password credentials. 
    // Change database named `rpdelete6` credentials
    // to `Neil` and `J*bzNgXlZqV24`
    // The public/private status of the DB name is persisted.
    DBName.ChangeCredentials('rpdelete6', 'Neil', 'J*bzNgXlZqV24')
