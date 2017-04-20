Ansible Role: Wordpress
=========

Role for Wordpress installation on the server, currently designed to work on Ubuntu Xenial.

Requirements
------------

There are no special requirements for now.

Role Variables
--------------
The following topic contains 3 sections: Important, Default and Extra variables.

### Important Variables
In this section there are listed variables that you should define using this role.

    wp_install_path: ''
Here you should input full local path to the folder where WordPress should be installed (without trailing slash).

```
wp_db_name: ''
wp_db_user: ''
wp_db_password: ''
wp_db_host: ''
```
Those variables are responsible for WordPress database connection settings, fill them according to [documentation](https://codex.wordpress.org/Editing_wp-config.php#Configure_Database_Settings).

### Default variables
These are variables that are listed in `default/main.yml` and can also be overwritten in your own variables.

    wp_release: ''
Changing this variable you can choose which WordPress release version to install. You should use form like `wordpress-4.7` or `wordpress-4.7.3`. Default value is `latest` and will download latest stable version from [WordPress official website](http://wordpress.org/download).

    wp_add_configuration_file: ''
This is a boolean variable that decides whether to add `wp_config.php` file, if you will choose `false` then all other configuration variables won't have any effect. Default value is `true`.

    wp_overwrite_release: '' # Boolean
If there is already existing WordPress release, in the path you've entered in the `wp_install_path` variable and you want to overwrite it, set this variable to `true`. By default it is set to `false`.

    wp_automatic_updater_disabled: '' #Boolean
Set to `false` if you want to enable WordPress auto updates. Default is `true`.

```
wp_auth_key: "W%|Z{rL+6fxXpu6@0bQ-9n|u@oB?~<%?yG-j05*y2!N_:.r9hGl<#(o/:U6lSxJC"
wp_secure_auth_key: "M|5?y:3%zR9ZD[Pr6iT6CVubU.j-3~Y>+XMqxdW+Q [rFFw5(53aoj|ig]m3/1%b"
wp_logged_in_key: ";JsZU|:#-s-F!yW<!L|{cPt+IPK*uW+E6Ime5TJjm0(^mEFwk2O_D+ZA|Z*SG{~d"
wp_nonce_key: "X~+9aGddCX)S` pL_Bl7e|?zp`#cO:$4m|_}c0B8?.+&+e^`A-<v(PhAsK?sVu:|"
wp_auth_salt: "Ag3WbMhb``xrkg.Htk|o1p6PAN0F[80/>d--C&rpw2bTiJ~U+Vqx+1eEC@pAQ]^s"
wp_secure_auth_salt: "+uIao-KHo+sVD;c6/B@q}[n-u5{E&o{><MK{FV9`Dk#xq</bimkV?bxKDIy* PMM"
wp_logged_in_salt: "$<kD*32hi!b$hW{&P<_E>)fq7?YivNg*RHoyKktn|ZHpHA=2ajv3ME@MF:uICT|-"
wp_nonce_salt: "#NE_|qi>xa|_6ObI`OjF2(J|m}4}.]9{{ '{#' }}9dlXAjfsa~6|vFP[;ap-Z2$CwUh?]$k"
```
Default generated for values of Security keys configuration, I would recommend to change them when you will be using this role in production, they can be generated on this [page](https://api.wordpress.org/secret-key/1.1/salt/).  Here you can see, that in case, when there will be generated some Jinja2 template structures they should be escaped (eg. `{#` shoud be escaped as `{{ '{#' }}`).
    
### Extra variables
These are variables that are not mentioned in the `default/main.yml` but still can be used if you have such a necessity.

    wp_enable_config_backup: ''
When adding configuration file with this script, if there already was a `wp-config.php` file it will be overwritten. If the variable above is set to `true`, then the previous version of `wp-config.php` will be saved in the same directory with timestamp, so you will have backup. Default value is `true`.

```
wp_enable_debug: '' # Boolean
wp_script_debug: '' # Boolean
wp_debug_log: '' # Boolean
wp_debug_display: '' # Boolean
wp_debug_savequeries: '' # Boolean
```
These are variables related to debugging. `wp_enable_debug` is boolean variable, set it to `true` if you are going to use Debug mode in WordPress, then you will other variables related to Debugging will have some effect.
If you will enable debugging by default `WP_DEBUG_LOG` and `WP_DEBUG_DISPLAY` will be set to `true` and `false`, respectively, until you will change them. That means, that all errors notices and warnings will be logged in `debug.log` file, located in `wp-content` folder.

```
wp_db_charset: 'utf8' # Database character set
wp_db_collate: '' # Database collation
wp_db_table_prefix: 'wp_' # String that is placed in front of database tables.
```
Self-explanatory variables.

```
wp_siteurl: '' # String
wp_home: '' # String
wp_content_dir: '' # String
wp_plugin_dir: '' # String 
wp_themes_dir: '' # String
wp_uploads_dir: '' # String
wp_autosave_interval: '' # Int
wp_post_revisions: '' # Int
wp_concatenate_scripts: '' # Boolean
wp_memory_limit: '' # Int
wp_max_memory_limit: '' # Int
wp_include_advanced_cache: '' # Boolean
wp_custom_user_table: '' # String
wp_custom_user_meta_table: '' # String
wp_empty_trash_days: '' # Int
wp_allow_repair: '' # Boolean
wp_disallow_file_edit: '' # Boolean
wp_disallow_file_mods: '' # Boolean
wp_force_ssl_admin: '' # Boolean
wp_auto_update_core: '' # Boolean
wp_image_edit_overwrite: '' # Boolean
wp_disallow_unfiltered_html: '' # Boolean
```
All the needed information about those variables can be found on [Editing wp-config.php website](http://codex.wordpress.org/Editing_wp-config.php). By default they are omitted, but you can use them when needed.
Note! When changing directories paths you should use FULL local path of the directory (without trailing slash).

Dependencies
------------

This role doesn't have any dependencies.

Example Playbook
----------------

```
- hosts: localhost
  become: yes
  roles:
    - { role: 1nfinitum.wordpress }
```
License
-------

MIT

Author Information
------------------

This role was created in 2017 by [Mykhaylo Kolesnik](http://github.com/1nfinitum).
