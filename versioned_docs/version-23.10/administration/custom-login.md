---
id: customize-centreon
title: Customize Centreon
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

You can customize some elements of your Centreon platform:

- the login page: you can change the background and the logo, and add a text.
- you can define a name for your platform (e.g. **Test**, **Production**, etc.), which will be displayed in the banner once you are logged in.

To be able to customize your Centreon platform, you need to install the **Centreon IT Edition Extensions** extension.

> **Centreon IT Edition Extensions** is a Centreon extension that requires a valid [license](../administration/licenses.md).
> To purchase one and retrieve the necessary repositories, contact [Centreon](mailto:sales@centreon.com).

## Installation

1. Install the Centreon Business repository. You can find its address on the
[support portal](https://support.centreon.com/hc/en-us/categories/10341239833105-Repositories).

2. Install the package using the following command:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

``` shell
dnf install centreon-it-edition-extensions
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

``` shell
dnf install centreon-it-edition-extensions
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
apt update && apt install centreon-it-edition-extensions
```

</TabItem>
</Tabs>

3. Go to **Administration > Extensions > Manager** and click the install button for the following modules:

   - **License Manager** (if not yet installed)
   - **IT Edition Extensions**

## Configuration

Go to **Administration > Customize Centreon**. The options are:

- **Platform name**: define a name for your platform, e.g. **Test**, **Production**, etc. This name will be visible both on the login page (next to the logo), and in the banner once you are logged in.
- **Select a logo**: replace the Centreon logo on the login page (but not in the top left corner once you are logged in). Before you can select a logo in this field, you need to add the file to your platform's [media](./parameters/medias.md).
- **Select a background**: replace the default background. Before you can select a background in this field, you need to add the file to your platform's [media](./parameters/medias.md).
- **Insert your presentation text**: enter a text to be displayed in the login area.
- **Your text position**: define where the custom text will be displayed, if defined (above the word **Login** or below the **Connect** button).

Check what your login page will look like in the **Preview**. When you're happy with it, click **Save**.