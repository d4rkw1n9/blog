---
title: Siyuan
date: '2025-04-24 02:53:33'
permalink: /post/siyuan-z1en3dl.html
tags:
  - siyuan
categories:
  - Homelabbing
layout: post
published: true
---



# Siyuan

This is just a sample note, retrieved from siyuan publisher plugin.

Documentary tree

* Publishing tool platform configuration guide

  * Github platform configuration guide

    * Hexo platform configuration guide

 Hexo platform configuration guide

 Official Network

[ https://hexo.io/zh-cn/  ](https://hexo.io/zh-cn/)

 preparation

bash

```solidity
 npm install hexo-cli -g
 hexo init hexo-blog
 cd blog
 npm install
 hexo server
```

 Hexo's Front-matter

[ Front-matter | Hexo  ](https://hexo.io/zh-cn/docs/front-matter)

 I develop a test blog for this function: [ https://hexo.terwer.space  ](https://hexo.terwer.space/)

 source code: [ https://github.com/terwer/hexo-blog  ](https://github.com/terwer/hexo-blog)

 Publishing guide

 Basic settings

 Platform introduction

1. ‍

 Introducing the Hexo platform (if Gitlab is used, Gitlab needs to be deployed by itself, Gitlabhexo needs to be imported, others are similar, the course takes Github as an example)

 Click the release tool icon:

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvVGtEelI4Sk9CeEhDQTF2LnBuZw==)

 Choose in turn  ** General settings **  ->  ** Post settings. **

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvZnZUVjlCUjVVeU9odG5qLnBuZw==)

 Click in sequence in the popped conversation box  ** Box store **  ->  ** Github **  ->  ** Hexo ** , Click in the popped drawer  ** Enable ** ,then  ** submit: **

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvRmprWTRDc09NSmd0OUFxLnBuZw==)

 Note: This is the first time it has been added. Because multiple examples are currently supported, if it is the second time, a self-defined setting name can be added.

 Then close the bullet window. Click again  ** General settings **  ->  ** Posting settings ** , You can see the newly added platform in the list.

 Note: It is strongly recommended to reopen to avoid the possibility of unsynchronized configuration.

2. ‍

 Click  ** General settings **  ->  ** Post settings, ** Find the new Hexo platform.

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvMVlxWmVnT3pCTVVJczdOLnBuZw==)

3. ‍

 Set the minimum available configuration

 Click  ** Set **  Enter the platform to set the interface. In general, the following paragraphs are necessary. Other configurations may be modified as appropriate.

 Configuration 1

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvRW9CZ2tuTzI0aUdkVFd2LnBuZw==)

 Configuration 2

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvTlFuOEJMZXIzWk1KNjdZLnBuZw==)

 Configuration 3-More configuration (optional)

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvTVRJZ3kyY1pPQTNWWWRRLnBuZw==)

4. ‍

 After the correct configuration, it is shown as follows:

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvQXRsUUJ1REUyOHN2b2o5LnBuZw==)

5. ‍

 Start publishing, directly  ** One key release **  ->  ** hexo **  That's it.

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvdFJHdkY2Qnd5T0NVejdiLnBuZw==)

 Successful reminder

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvU3hDZTdJVDhuaWt0NXFwLnBuZw==)

6. ‍

 Regular release, support more personalized settings, click  ** Regular release **  ->  ** Hexo ** Then go in and post it after personalized settings.

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvMnd0RDNFY2lHZTVwS0NsLnBuZw==)

7. ‍

 Delete or disassociate

 After successful release  ** delete **  or  ** Unassociated ** , ** Can only be used in routine release operations ** .

** delete ** :Corresponding"  cancel  "Button, delete the remote article first, and then release the remote connection with the local area.

** Unassociated ** :Corresponding"  Mandatory deletion  "Buttons, forced to release the association, regardless of whether the remote article is deleted.  This function can also be used for repairs after remote articles have been deleted to facilitate second release  .

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvbG8ya1k3NnJEbTkxaVdmLnBuZw==)

 Advanced personalized settings

 Published catalog

 The default is   source/_posts  , If you need to modify, please follow Hexo official instructions

 Graphical services and photo storage paths  ^ v1.34.0+ ^

1. ‍

 No drawing  , Not processing pictures

2. ‍

 PicGo  , Use the absolute path of the graphical bed

3. ‍

 Current platform  , Can be set at this time  ** Picture storage path **  with  ** Picture link address **

** Picture storage path ** :Pictures, silently think   source/images  ,  General situation does not recommend modification  , If modified, please set to   source/xxx

** Picture link address ** : The picture path cited in the document, this platform and ** Picture storage path ** Just keep it consistent, that is   images   ,  General situation does not recommend modification  , If modified, please correspond.

[ Hexo Global Resource Folder ](https://hexo.io/zh-cn/docs/asset-folders#%E5%85%A8%E5%B1%80%E8%B5%84%E6%BA%90%E6%96%87%E4%BB%B6%E5%A4%B9)

![image](https://img1.siyuan.wiki/api/vip/open/media/aHR0cHM6Ly9jZG4uc2EubmV0LzIwMjUvMDQvMTUvY0I4MXZhUGd4aWQycmhHLnBuZw==)

 Document rules

 The path does not support dynamic configuration for the time being, but it can be achieved by self-defined file name rules ^ v1.29.1+ ^ .

** Basic configuration **

 Document rules: [yyy]/[MM]/[filename].md

 Among them, the occupiers can be replaced dynamically as follows:

 [yyyy]   Year, for example: 2025

 [MM]   Month, for example: 02

 [mm]

 [dd]   Days, for example: 26

 [slug]   Alias, for example: test-document-xdfr45f

 [filename]   File name, for example: test document

 For example: [filename].md, [slug].md, [yyy]-[mm]d[-]slug[

 Linking characters can only be  `` / `-` _ `.` ~ ``​ Everything else will be removed.

** Classification and labeling **

 For classification and labeling, add two variables

 [category]   Get the first classification, not ignored

 [cats]   All categories are combined

 [tag]   Get the first label, not ignored

 [tags]   All labels are combined

 YAML preset

 Preview rules

[Document outline]()

[Official Network]()

[preparation]()

[Hexo&apos;s Front-matter]()

[Publishing guideBasic settingsPlatform introduction]()

[Advanced personalized settingsPublished catalog]()

[Graphical service and picture storage path v1.34.0+]()

[Document rules]()

[YAML preset]()

[Preview rules]()
