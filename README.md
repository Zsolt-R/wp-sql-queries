# wp-sql-queries
Useful WordPress SQL Queries

##### ADD USER

Database name: 		  database_name  
User name: 	   		  new.user.name  
User Password: 		  new_password  
User display name:  User Nicename  
User Email:         email@domain.com  
User Display Name:  User D.

    INSERT INTO `database_name`.`wp_users` (`ID`, `user_login`, `user_pass`, `user_nicename`, `user_email`, `user_url`, `user_registered`, `user_activation_key`, `user_status`, `display_name`) VALUES ('9999', 'new.user.name', MD5('new_password'), 'User Nicename', 'email@domain.com', 'http://www.domain.com/', '2015-11-27 00:00:00', '', '0', 'User D.');
    INSERT INTO `database_name`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '9999', 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');
    INSERT INTO `database_name`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '9999', 'wp_user_level', '10');

##### MOVE DB

Old domain Name: www.olddomainname.com / olddomainname.com  
New domain Name: newdomainname.com

    UPDATE wp_options SET option_value = replace(option_value, 'www.olddomainname.com', 'newdomainname.com') WHERE option_name = 'home' OR option_name = 'siteurl';
    UPDATE wp_posts SET guid = replace(guid, 'www.olddomainname.com','newdomainname.com');
    UPDATE wp_posts SET post_content = replace(post_content, 'www.olddomainname.com', 'newdomainname.com');
    UPDATE wp_postmeta SET meta_value = REPLACE (meta_value, 'www.olddomainname.com','newdomainname.com');
    
##### Bulk change post meta_key
    UPDATE wp_postmeta SET meta_key = 'new_key_name' WHERE meta_key = 'old_key_name';

##### Change WP database table prefix

###### Step 1. RENAME ALL WORDPRESS DATABASE TABLES

    RENAME table `wp_commentmeta` TO `wp_ newprefix_commentmeta`;
    RENAME table `wp_comments` TO `wp_ newprefix_comments`;
    RENAME table `wp_links` TO `wp_ newprefix_links`;
    RENAME table `wp_options` TO `wp_ newprefix_options`;
    RENAME table `wp_postmeta` TO `wp_ newprefix_postmeta`;
    RENAME table `wp_posts` TO `wp_ newprefix_posts`;
    RENAME table `wp_terms` TO `wp_ newprefix_terms`;
    RENAME table `wp_termmeta` TO `wp_ newprefix_termmeta`;
    RENAME table `wp_term_relationships` TO `wp_ newprefix_term_relationships`;
    RENAME table `wp_term_taxonomy` TO `wp_ newprefix_term_taxonomy`;
    RENAME table `wp_usermeta` TO `wp_ newprefix_usermeta`;
    RENAME table `wp_users` TO `wp_ newprefix_users`;
    
###### Step 2. MODIFY THE OPTIONS TABLE

    SELECT * FROM `wp_ newprefix_options` WHERE `option_name` LIKE '%wp_%'
    
###### Step 3. MODIFY THE USERMETA TABLE

    SELECT * FROM `wp_ newprefix_usermeta` WHERE `meta_key` LIKE ‘%wp_%’
