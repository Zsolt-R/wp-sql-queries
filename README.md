# wp-sql-queries
Useful WordPress SQL Queries

////////////////////
//	ADD USER
////////////////////

Database name: 		  database_name  
User name: 	   		  new.user.name  
User Password: 		  new_password  
User display name:  User Nicename  
User Email:         email@domain.com  
User Display Name:  User D.

    INSERT INTO `database_name`.`wp_users` (`ID`, `user_login`, `user_pass`, `user_nicename`, `user_email`, `user_url`, `user_registered`, `user_activation_key`, `user_status`, `display_name`) VALUES ('9999', 'new.user.name', MD5('new_password'), 'User Nicename', 'email@domain.com', '', '2015-11-27 00:00:00', '', '0', 'User D.');
    INSERT INTO `database_name`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '9999', 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');
    INSERT INTO `database_name`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '9999', 'wp_user_level', '10');


##	MOVE DB

Old domain Name: www.olddomainname.com / olddomainname.com  
New domain Name: newdomainname.com

    UPDATE wp_options SET option_value = replace(option_value, 'www.olddomainname.com', 'newdomainname.com') WHERE option_name = 'home' OR option_name = 'siteurl';
    UPDATE wp_posts SET guid = replace(guid, 'www.olddomainname.com','newdomainname.com');
    UPDATE wp_posts SET post_content = replace(post_content, 'www.olddomainname.com', 'newdomainname.com');
    UPDATE wp_postmeta SET meta_value = REPLACE (meta_value, 'www.olddomainname.com','newdomainname.com');
