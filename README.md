secret-octo-wight
=================

Pod user_id

secret-octo-wight. 

I created a pod field entitled: user_id and set it as a relationship as WP User. But the helper code for auto_set_current_user sets the field for selection but when I try to select another user so the user can add the info it goes back to administrator. I need to be able to set the user.

I changed the manage_content.php as directed in answer: http://podscms.org/qna/questions/2186 the code is below:

Basically,I just went to manage_content.php, line 15 and added this: // If user is logged in, store user_id

if( is_user_logged_in() ) { global $current_user; $user_id = $current_user->ID; }

It just gets the logged-in user's wordpress user_id. Then, in about line 315 or so, I replaced the existing elseif statement with the following: elseif (pods_access('pod_' . $dtname) && !empty($user_id)) { if( current_user_can('administrator') ) { pods_ui_manage('pod=' . $dtname .'&sort=p.modified DESC' . ('top-level-manage' != $manage_action ? '&session_filters=false' : '')); } else { $management_options = array('pod' => $dtname, 'edit_where' => array('user_id' => $user_id), 'sort' => 'p.modified DESC'); pods_ui_manage($management_options); }