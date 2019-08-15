# Callguard Hosted Panel Setup Guide : Part 2

The following is a project environment setup and installation guide, for developerss who are unfamiliar with Eckoh's **Callguard Hosted Panel** (CGH) project.

Part 2 covers the following:

- Syndication file

- Something

- Something

Do not proceed unless you have already completed CGH: [Part 1](deadlink) 

### Syndication file

------









Go to your syndication.xml file NOT the install

Add your domain names to the <CLIENT-**></CLIENT-**> tags - MAKE SURE the client numbers are correct!!! to co-inside with the client number allocated in the database (in this case 44) CHECK THIS IN SEQUELPRO DB!!!!!!!
AND that you have a domain with the VERSION number in it

```
<DEV>
    <!-- </CLIENT-update> --> <!-- uncomment this tag at setup -->
    <CLIENT-21><!-- used only for setup: REMOVE and REPLACE with ABOVE, update as appropriate for project -->
        <!-- Test WebPanel -->
        <domain>update-project-name.54.dev.eckoh.com</domain>
        <domain>update-version-number.54.dev.eckoh.com</domain>
    <!-- </CLIENT-update> --> <!-- uncomment this tag at setup -->
    <CLIENT-21><!-- used only for setup: REMOVE and REPLACE with ABOVE, update as appropriate for project -->
</DEV>
```

DO NOT USE ‘.’ easily!!! - they represent subfolders in urls and eckoh servers sometimes struggle with interpretation, but ‘_’ / ‘-‘ are fine
ONLY USE .com
INCLUDE “.54.dev.eckoh” at the end
So in the end you should get something like:

```
<DEV>
    </CLIENT-44><!-- uncomment this tag at setup -->
        <!-- Test WebPanel -->
        <domain>example-project.54.dev.eckoh.com</domain>
        <domain>update-version-number.54.dev.eckoh.com</domain>
    </CLIENT-44><!-- uncomment this tag at setup -->
</DEV>
```

Copy and paste Client and Domain tags into UAT and Prod/Prod_ix/Prod_sa sections as appropriate - make sure you place “UPDATE”’s in the relevant sections for your RFC later!

```
<UAT>
</UAT>

<PROD_IX>
</PROD_IX>

<PROD_SA>
</PROD_SA>
```

BECOMES:

<UAT>
        <CLIENT-update>
            <!-- Test WebPanel -->
            <domain>update</domain>
            <domain>update</domain>
        </CLIENT-update>
    </UAT>

etc etc…

<?xml version="1.0" encoding="UTF-8"?>
<syndications>
<DEV>
    <!-- </CLIENT-update> --> <!-- uncomment this tag at setup -->
    <CLIENT-21><!-- used only for setup: REMOVE and REPLACE with ABOVE, update as appropriate for project -->
        <!-- Test WebPanel -->
        <domain>update-project-name.dev-secweb.eckoh.com</domain>
        <domain>update-version-number-update-project-name.dev-secweb.eckoh.com</domain>
    <!-- </CLIENT-update> --> <!-- uncomment this tag at setup -->
    <CLIENT-21><!-- used only for setup: REMOVE and REPLACE with ABOVE, update as appropriate for project -->
</DEV>
<UAT>
    <CLIENT-update>
        <!-- Test WebPanel -->
        <domain>update-project-name.uat.eckoh.com</domain>
        <domain>update-version-number-update-project-name.uat.eckoh.com</domain>
    </CLIENT-update>
</UAT>
<PROD_IX>
    <CLIENT-update>
        <domain>update-project-name.eckoh.com</domain>
        <domain>update-version-number-update-project-name.eckoh.com</domain>
    </CLIENT-update>
</PROD_IX>
<PROD_SA>
    <CLIENT-update>
        <domain>update-project-name.production.eckoh.com</domain>
        <domain>update-version-number-update-project-name.production.eckoh.com</domain>
    </CLIENT-update>
</PROD_SA>/

////////// syndication.xml

////////// syndication.xml.install

Copy over the below - make sure you UPDATE the CLIENT ID AND the actual DOMAIN NAME to what you used in the syndication.xml file previously

</syndications>

while PROD_SA is not in use atm it is good to make your panels “future” ready

////////// syndication.xml.install

