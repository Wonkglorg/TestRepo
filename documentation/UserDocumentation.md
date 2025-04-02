# MarkDoc

<img src="/resources/images/logo_x250.png" alt="startSite" width="250" />


## User manuel

---

## 📚 Table of Contents

- **[1. Overview](#Overview)**
- **[2. Introduction](#Introduction)**
- **[3. Core Components](#core-components)**
   - [Navigation at the top](#navigation-at-the-top)
   - [Sidebar on the left](#sidebar-on-the-left)
   - [Main window in the middle](#main-window-in-the-middle)
   - [PopUps](#PopUps)
- **[4. Login](#login)**
- **[5. Add New Resource](#add-new-resource)**
   - [Upload](#upload)
   - [Create empty resource](#create-empty-resource)
- **[6. Resource Tagging](#resource-tagging)**
   - [Edit repo tags](#edit-repo-tags)
   - [Edit resource tags](#edit-resource-tags)
   - [Resource information](#resource-information)
- **[7. Browse Resource](#browse-resource)**
   - [Content search](#content-search)
   - [Path search](#path-search)
   - [Tag filter](#tag-filter)
- **[8. Edit Resource](#edit-resource)**
- **[9. Admin Management](#admin-management)**
   - [User management](#user-management)
      - [Add user](#add-user)
      - [Add/remove user to/from groups](#addremove-user-tofrom-groups)
   - [Group management](#group-management)
      - [Add Group](#add-group)
      - [Add/remove users to/from group](#addremove-users-tofrom-group)
   - [Permission management](#permission-management)
      - [User Permission](#user-permission)
      - [Group Permission](#group-permission)



<div style="page-break-after: always;"></div>

## Overview

**Project Name:** MarkDoc
**Version:** 1.0.0
**Authors:** Feldinger Niklas
**Date:** 2025-03-29
**Purpose:** Web-based tool for creating and managing project documentation.
**Scope:** This tool is intended for developers, technical writers, and project managers to collaboratively manage
project documentation using markdown. It includes permission access control and quality of life markdown editing.

## Introduction

Welcome to the MarkDoc User Manual. 
This guide is designed to help you understand and effectively use the application. 
Whether you are a new user or an experienced one, this manual provides step-by-step instructions, feature overviews, 
and troubleshooting tips to ensure a smooth experience.

---

## core components

<img src="/resources/images/frontend/startSite.png" alt="startSite" width="1100" />

### Navigation at the top

1. Toggle button for the sidebar
2. Logo
3. Searchbar to search file data or paths
4. Profil dropdown to login with different users

### Sidebar on the left

1. Dragable to resize the bar
2. Filetree with all repositories, pahts and .md resourcen
3. Resource upload button to upload word or markdown file
4. Create new resource button to create a new, empty resource
5. Admin button to navigate to the admin management site. Only visible as admin

### Main window in the middle

1. Editor to edit in markdown
2. View/preview to see formated file data, the resource path and tags
3. Admin component to manage groups, users and permissions

### PopUps

The user input is done with popUps with three different types of input. 
1. Casual input field where you can type freely.
2. Drop down with fix inputs
3. Some dropdowns, have a custom selection "More..." where an extra input field opens and you can write more than one value with a specific pattern: value1;value2;value3

<img src="/resources/images/frontend/pupUpExample.png" alt="login" width="250" />

<div style="page-break-after: always;"></div>

---

## Login

In this version of MarkDoc, there is no login window.
There are two users to choose. One with admin rights and one without.
you can choose between them in the top right corner.

<img src="/resources/images/frontend/login.png" alt="login" width="250" />

---

## Add new Resource

You can create new Resources in two ways. Either upload an existing word (.docx) or markdown (.md) file from your computer, or create a new empty resource.

### Upload

For uploading a file, click on the symbol in the left bottom corner and choose a file.

<img src="/resources/images/frontend/upload.png" alt="upload" width="150" />

After that a popUp appears:

1. Required - Choose a repo from the dropdown
2. Optional - Write in the input a category
3. Optional - Chose 1 tag from dropdown or choose "More..." and add more than 1 tags with the pattern: tag1;tag2;tag3 ...
4. Upload

<img src="/resources/images/frontend/uploadPopUp.png" alt="uploadPopUp" width="250" />

### Create empty resource

For creating a new empty resource, click on the second symbol in the left bottom corner.

<img src="/resources/images/frontend/createNew.png" alt="createNew" width="150" />

A popUp appears:

1. Required - write down the path where you want to save the resource.
   Example: path1/path2/resourceName
2. Required - choose a repository
3. Optional - Type in a category
4. Optional - Chose 1 tag from dropdown or choose "More..." and add more than 1 tags with the pattern: tag1;tag2;tag3 ...

<img src="/resources/images/frontend/createNewPopUp.png" alt="createNewPopUp" width="250" />

---

## Resource tagging

With the tagging feature, you can mark resources to group and find them easier
Tags are NOT created global instead you create them on a repo and use them on resources in the repo.

### Edit repo tags

In order to tag a resource, you have to create a tag on its repository.
To do this, hover over a repo in the resource tree, click the three dots and click edit tags.

<img src="/resources/images/frontend/createTagOnRepo.png" alt="createTagOnRepo" width="250" />

Fill out the popUp:
1. Enter the tagId
2. Enter a name for the tag
3. You can also choose tags to remove from a repo

<img src="/resources/images/frontend/addTagOnRepoPopUp.png" alt="addTagOnRepoPopUp" width="250" />

### Edit resource tags

To tag a resource, hover over a resource in the resource tree, click on the three dots and click edit tags.

<img src="/resources/images/frontend/addTagsOnResource.png" alt="addTagsOnResource" width="250" />

Fill out the popup to add or remove tags on a resource

1. To add tags chose 1 tag from dropdown or choose "More..." and add more than 1 tags with the pattern: tag1;tag2;tag3 ...
2. To remove tags chose 1 tag from dropdown or choose "More..." and remove more than 1 tags with the pattern: tag1;tag2;tag3 ...

<img src="/resources/images/frontend/addTagsOnResourcePopUp.png" alt="addTagsOnResourcePopUp" width="250" />

### Resource information

There is another way to edit tags on resources by the resource information.
Just select a resource from the tree and above the preview you can see information about this resource.
1. The repository
2. The full path
3. All tags on this resource
4. Edit tags on this resource

<img src="/resources/images/frontend/resourceInformation.png" alt="resourceInformation" width="500" />

---

## Browse resource

In the search bar on the top centered navigation component, you can search for resources and filter with tags.

### Content search

The standard is in file search. Just enter text you want to search in all resources content and hit enter. 
When results found, a dropdown appears with all the resources containing the search term in its data.
Clicking the result, you will be navigated to the resource.

<img src="/resources/images/frontend/inFileSearch.png" alt="inFileSearch" width="350" />

### Path search

If you want to search for resources path, you use the same search bar.
Just put the '$' in front and search with the ant path style pattern. It lists all resources with a matching path.
https://stackoverflow.com/questions/2952196/ant-path-style-patterns

<img src="/resources/images/frontend/pathSearch.png" alt="pathSearch" width="350" />


### Tag filter

For both content search and ant path pattern search, you can moreover filter the results with tags.
Therefor click the arrow on the end of the search bar and choose you option.

1. Checking tags, list only specific resources with this marked tag.
2. Denying tags, list only resources that are specific not marked with this tag.
3. Tags you don´t want to filter leave empty.

<img src="/resources/images/frontend/tagFilter.png" alt="tagFilter" width="350" />

---

## Edit Resource

With the build in markdown editor in our web application, editing resources is quit easy.
1. Select a resource and click on the editor button on the top
2. Start writing you markdown documentation
3. View with the preview option
4. Dont forget to save!

<img src="/resources/images/frontend/editResourceButton.png" alt="editResourceButton" width="350" />
  
<img src="/resources/images/frontend/editor.png" alt="editor" width="1100" />

---

## Admin management

In order to get to the admin area, you have to be logged on as admin.
Click on the admin button in the left bottom corner.

<img src="/resources/images/frontend/adminButton.png" alt="adminButton" width="150" />

Navigate in the admin area with these buttons and dropdown.

<img src="/resources/images/frontend/permissionNavigation.png" alt="login" width="500" />


### User management

Users are global, have a role and can be added to groups.

#### Add user

Click in the user management component on Add User

<img src="/resources/images/frontend/addUser.png" alt="addUser" width="250" />

Fill out the pop-up
1. Required - enter userId
2. Required - enter password
3. Required - repeat password
4. Required - choose one of two roles - admin or user
5. Optional - add user to one or more groups

<img src="/resources/images/frontend/addUserPopUp.png" alt="addUserPopUp" width="250" />

#### Add/remove user to/from groups

Click on the edit icon next to the user you want edit.

<img src="/resources/images/frontend/editUser.png" alt="editUser" width="250" />

Fill out the pop-up
1. Choose one or more existing groups you want to add the user.
2. Choose one or more groups where you want to remove the user from.

<img src="/resources/images/frontend/editUserPopUp.png" alt="editUserPopUp" width="250" />

### Group management

#### Add Group

Click in the user management component on Add Group

<img src="/resources/images/frontend/addGroup.png" alt="addGroup" width="250" />

Fill out the pop-up
1. Required - enter groupId
2. Required - enter groupName
3. Optional - add one or more users to the group

   <img src="/resources/images/frontend/addGroupPopUp.png" alt="addGroupPopUp" width="250" />

#### Add/remove users to/from group

Click on the edit icon next to the group you want edit.

<img src="/resources/images/frontend/editGroup.png" alt="editGroup" width="250" />

Fill out the pop-up
1. Choose one or more existing users you want to add to the group.
2. Choose one or more users where you want to remove from the group.

<img src="/resources/images/frontend/editGroupPopUp.png" alt="editGroupPopUp" width="250" />

### Permission management

Permissions are individually set on repos and paths.

There are 4 different types of permission
1. ADMIN
2. EDIT
3. VIEW
4. DENY

You can add them to users and groups, where user permissions have a greater value than group permissions.

#### User Permission

1. select a repository
2. select a user

<img src="/resources/images/frontend/permissionManagementUser.png" alt="permissionManagementUser" width="400" />

To add a user permission, click on the button.

<img src="/resources/images/frontend/addUserPermission.png" alt="addUserPermission" width="250" />

A pop-up appears:
1. Required - choose a user on whom the permission should be set
2. Required - choose one of four permission types
3. Required - add the path the permission should be applied - ant path possible

<img src="/resources/images/frontend/addUserPermissionPopUp.png" alt="addUserPermissionPopUp" width="250" />

To edit a users permission click the symbol next to the permission

<img src="/resources/images/frontend/editUserPermission.png" alt="editUserPermission" width="250" />

A pop-up appears
1. Change the user on whom the permission should be set
2. Change the permission type
3. You can not change the path.

<img src="/resources/images/frontend/editUserPermissionPopUp.png" alt="editUserPermissionPopUp" width="250" />


#### Group Permission

1. select a repository
2. select a group

<img src="/resources/images/frontend/permissionManagementGroup.png" alt="permissionManagementGroup" width="400" />

To add a group permission, click on the button.

<img src="/resources/images/frontend/addGroupPermission.png" alt="addGroupPermission" width="250" />

A pop-up appears:
1. Required - choose a group on whom the permission should be set
2. Required - choose one of four permission types
3. Required - add the path the permission should be applied - ant path possible

<img src="/resources/images/frontend/addGroupPermissionPopUp.png" alt="addGroupPermissionPopUp" width="250" />

To edit a group permission click the symbol next to the permission

<img src="/resources/images/frontend/editGroupPermission.png" alt="editGroupPermission" width="250" />

1. Change the group on whom the permission should be set
2. Change the permission type
3. You can not change the path.

<img src="/resources/images/frontend/editGroupPermissionPopUp.png" alt="editGroupPermissionPopUp" width="250" />

---
