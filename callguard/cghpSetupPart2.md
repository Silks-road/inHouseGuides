# Callguard Hosted Panel Setup Guide : Part 2

The following is a project environment setup and installation guide, for developerss who are unfamiliar with Eckoh's **Callguard Hosted Panel** (CGH) project.

**CGHP Part 2** covers setup for the following:

1. Syndication.xml.install
2. Vhost.conf.install
3. Vhost.conf

Do not proceed unless you have already completed [CGHP: Part 1](deadlink)

### Syndication.xml.install

------

#### Syndication.xml

Make a copy of the `syndication.xml.install` file **WITHOUT the extention**, including all content:

```
cp syndiaction.xml.install syndiaction.xml
```

#### Client No. & Service ID tags

Open your text editor and go to your `syndication.xml.install` file.

Within the `<DEV>` section, take your relevant **Client Number** and **Service ID** from your `config.xml` file and repleat the process of updating the `<CLIENT-##>` tags throughout this file:

> **NOTE**: If you are unsure about this process, see [CGHP: Part 1](linktocghpart1) - Config file: Client No. & Service ID tags. the same RFC rules apply.

#### Creating test URLs

WIthin your `<CLIENT-##>` tags, you should see `<domain>` tags.

Your `<domain>` tags are where you add your project URL. Create a test domain name that is relevant to the client and project at hand, while in keeping with the Eckoh company [naming conventions guide](deadlink).

**Make sure to adhere to the following**:

- You have a minimum of at least two test URLs:
  - The first specifiys the client project name.
  - The second includes the client project name, _plus_ the current version number.
  - The version number _must_ come before the client project name.
- At least one domain must have { .54.dev.eckoh } in the URL.
- At least one domain must have { .dev-secweb.eckoh } in the URL.
- Only use the { .com } domain suffix.
- Use { _ } and { - } as seperators.

> **NOTE**: _DO NOT USE dot notation carelessly_ when creating your test URLs. All " . " seperation in Mande URLs are representative of subfolders, and as a result the Eckoh servers sometimes struggle with their interpretation.

The end product should be similar to the example given below:

```xml
<DEV>
  <CLIENT-44>
  	<!-- Test WebPanel -->
  	<domain>clothing-line-cgh-panel.54.dev.eckoh.com</domain>
  	<domain>clothing-line-cgh-panel.54.dev-secweb.eckoh.com</domain>
    <domain>1-3-8.clothing-line-cgh-panel.54.dev.eckoh.com</domain>
    <domain>1-3-8.clothing-line-cgh-panel.54.dev-secweb.eckoh.com</domain>
	</CLIENT-44>
</DEV>
```

Copy and paste the `<domain>` names/ tags into both the `<UAT>` and `<PROD>` sections, _but make sure to update the domain name suffixes, to keep each domain section relevant_.

You will notice that the `<PROD>` tags have extended to include `<PROD_IX>` and `<PROD_SA>`. If there are only `<PROD>` tags available, update them to `<PROD_IX>` and `<PROD_SA>` tags.

**Make sure to adhere to the following**:

- UAT end suffixes are UAT specific: { .uat.eckoh }
- PROD domain names are PROD _type_ specific:
  - `<PROD_IX>` : { .eckoh }
  - `<PROD_SA>` : { .production.eckoh }
  - Neither PROD sections need their version numbers included.

```xml
<UAT>
	<CLIENT-44>
  	<!-- Test WebPanel -->
    <domain>clothing-line-cgh-panel.uat.eckoh.com</domain>
    <domain>1-3-8.clothing-line-cgh-panel.uat.eckoh.com</domain>
	...
<PROD_IX>
  <CLIENT-44>
  	<domain>clothing-line-cgh-panel.eckoh.com</domain>
	...
<PROD_SA>
  <CLIENT-44>
    <domain>clothing-line-cgh-panel.production.eckoh.com</domain>
	...
```

All your domain name updates must be be included in your RFC.

> **NOTE**: While PROD_SA is not in use currently, it is good practice to include/ create this section in order to make your panels future proof.

## vhost.conf.install

Make a copy of the `vhost.conf.install` file **WITHOUT the extention**, including all content:

```
cp vhost.conf.install vhost.conf
```
