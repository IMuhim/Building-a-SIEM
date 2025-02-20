---
layout: default
---

Text can be **bold**, _italic_, or ~~strikethrough~~.

# Creating A Virtual Machine

Microsoft Azure can be accessed for free as a free trial is available for a limited amount of time. This project has been created using a Azure as it has all the tools required for this project. 

Firstly, I set up a virtual machine using the preset configuration. As part of setting up the virtual machine, I created the resource group "IMGroup" which acts as a container for everything created as part of this project. Crucially, I left the RDP port open as I will be generating RDP traffic, which is the most easily generated security event. 

After the virtual machine, "IstiakVM", is set up we can connect to it, view information such as which resource group it belongs to and what operating system it is running.

![Branching](1_VM_ss.png)

# Deploying Microsoft Sentinel

Once the virtual machine is set up, we need a log analystics workspace. This is can be done through Microsoft Sentinel. I created a log analytics workspace, "IstiakM-Log", in Microsoft Sentinel and added it to the "IMGroup" resource group set up earlier.

![Branching](2_Log_Analytics_Workspace.png)

After I created this workspace I added Microsoft Sentinel to the workspace. This is where incidents, automation and data will be presented, as shown below.

![Branching](7_Sentinel_Overview.png)

# Sending Data To Sentinel

The event logs of the virtual machine created previously need to be sent to the "IstiakM-Log" workspace. The workspace will then send the event log to sentinel.

This can achieved by setting up a data connector. This allows sentinel to get data from the event log of the virtual machine. I selected and installed the "Windows Security Events" connector from _Content Hub_.

![Branching](3_Install_Data_Connector.png)

Upon the installation of the connector, it show up in the list of data connectors under _Configuration_.

![Branching](3_Install_Data_Connector_Pt2.png)

# Creating Data Connection Rule

I created the rule "WindowsEventsToSentinel" within the "Windows Security Events via AMA" connector page and made sure to select the "IstiakVM" as this is where the data will be pulled from. The created will check for successful sign ins via RDP. The MITRE ATT&CK option will is set to _Initial Access_ as this is what I am monitoring. The rule is set to run every 5 minutes. The query used in this rule retrieves security events where a user was successfully able to brute froce access to the virtual machine, excluding any events related to system accounts. 


> The KQL query used in this rule:
> ```kql
> SecurityEvent 
> | where Activity contains "Success" and Account !contains "system"
> ```

![Branching](4_Creating_Data_Connection_Rule.png)

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
