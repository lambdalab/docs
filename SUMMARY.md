# Summary

* [Private Cloud Quick Installation](./enterprise/ON_PREM_INSTALL.md)
  * [Prerequisites](./enterprise/onpreinstall/PREREQUISITES.md)
  * [Install Docker and Docker Compose](./enterprise/onpreinstall/INSTALL_DOCKER.md)
  * [Authentication](./enterprise/onpreinstall/AUTHENTICATION.md)
  * [Clone Git Repo for Docker Compose](./enterprise/onpreinstall/CLONE_GIT_DOCKER_COMPOSE.md)
  * [Configure Kerberos Authentication](./enterprise/onpreinstall/CONFIGURE_KERBEROS.md)
  * [Download Docker Image and Start Docker Services](./enterprise/onpreinstall/DOWNLOAD_IMAGES.md)
  * [Upgrade Insight.io](./enterprise/onpreinstall/UPGRADE_INSIGHTIO.md)
  * [Deploy Insight.io with Multiple Machines](./enterprise/onpreinstall/DEPLOY_MULTIPLE_MACHINES.md)
  * [Common Process Management with Docker Compose](./enterprise/onpreinstall/COMMON_DOCKER_PROCESS_MANAGEMENT.md)
* [New User Guide](./enterprise/USER_GUIDE.md)
  * [Configure Github Integration](./enterprise/userguide/CONFIGURE_GITHUB_INTEGRATION.md)
  * [Configure Gitlab Integration](./enterprise/userguide/CONFIGURE_GITLAB_INTEGRATION.md)
  * [Configure BitBucket Server Integration](./enterprise/userguide/CONFIGURE_BITBUCKET_INTEGRATION.md)
  * [Configure LDAP Integration](./enterprise/userguide/CONFIGURE_LDAP_INTEGRATION.md)
  * [Configure SAML Integration](./enterprise/userguide/CONFIGURE_SAML.md)
  * [Configure Insight.io Browser Plugin for GitHub Enterprise](./enterprise/userguide/CONFIGURE_PLUGIN_GITHUB_ENTERPRISE.md)
  * [Configure Repositories Components](./enterprise/userguide/CONFIGURE_REPOS_COMPONENT.md)
  * [Create an Account](./enterprise/userguide/CREATE_ACCOUNT.md)
  * [Add Repository](./enterprise/userguide/ADD_REPOSITORY.md)
  * [Use Gitlab Plugin](./enterprise/userguide/USE_GITLAB_PLUGIN.md)
  * [Change settings.xml for Maven Project](./enterprise/userguide/MAVEN_CHANGE_SETTINGS.md)
  * [Customize Layout](./enterprise/userguide/CONFIGURE_CUSTOMIZED_LAYOUT.md)
  * [Customize Repository Build](./enterprise/userguide/CUSTOMIZE_REPOSITORY_BUILD.md)
  * [Obtain Code Analysis Log](./enterprise/userguide/OBTAIN_CODE_ANALYSIS_LOG.md)
  * [Use Api Access Token](./enterprise/userguide/USE_API_ACCESS_TOKEN.md)
  * [Configure Manual Update](./enterprise/userguide/CONFIGURE_MANUAL_UPDATE.md)
  * [Configure manual user permission management](./enterprise/userguide/CONFIGURE_MANUAL_USER_PERMISSION_MANAGEMENT.md)
  * [Configure Tracking](./enterprise/userguide/CONFIGURE_TRACKING.md)
* [API Documentation](./api/API.md)
  * [Authentication](./api/authentication/INDEX.md)
    * [Token Creation](./api/authentication/TOKEN_CREATION.md)
    * [Get All Tokens](./api/authentication/TOKEN_LIST.md)
    * [Revoke a Token](./api/authentication/TOKEN_REVOKE.md)
    * [Token Usage](./api/authentication/TOKEN_USAGE.md)
    * [Manage Token on UI](./api/authentication/TOKEN_MANAGEMENT_UI.md)
  * [Meta Data](./api/meta/INDEX.md)
    * [Get Meta Data](./api/meta/GET_META_DATA.md)
    * [Get Node Data](./api/meta/GET_NODE_DATA.md)
    * [Get References](./api/meta/GET_REFERENCES.md)
  * [Git Data](./api/git/INDEX.md)
    * [Get File Content](./api/git/GET_FILE_CONTENT.md)
    * [Get File List](./api/git/GET_FILE_LIST.md)
    * [Get Branches](./api/git/GET_BRANCHES.md)
    * [Get Tags](./api/git/GET_TAGS.md)
    * [Get Commits](./api/git/GET_COMMITS.md)
    * [Get Commit Diff](./api/git/GET_COMMIT_DIFF_VIEW.md)
    * [Get Blames](./api/git/GET_BLAMES.md)
  * [Projects](./api/projects/INDEX.md)
    * [Get Project Detailed Information](./api/projects/GET_PROJECT_INFO.md)
    * [Get All Projects in System](./api/projects/GET_ALL_PROJECTS.md)
    * [Get All Projects of User](./api/projects/GET_USER_PROJECTS.md)
    * [Get Recent Viewd Projects](./api/projects/GET_RECENT_PROJECTS.md)
    * [Get Starred Projects](./api/projects/GET_STARRED_PROJECTS.md)
    * [Get Project Analysis Log](./api/projects/GET_PROJECT_ANALYSIS_LOG.md)
    * [Configurate Project](./api/projects/CONFIG_PROJECT.md)
  * [User](./api/user/INDEX.md)
    * [Get User Profile](./api/user/GET_USER_PROFILE.md)
    * [Get Linked Services](./api/user/GET_LINKED_SERVICES.md)
    * [Manage Starred Files](./api/user/STAR_FILES.md)
    * [Manage Recent Visited Files](./api/user/RECENT_FILES.md)
    * [Manage Imported Projects](./api/user/MANAGE_IMPORTED_PROJECTS.md)
  * [Search](./api/search/INDEX.md)
    * [Get Typeahead Search](./api/search/GET_DATUM.md)
    * [Get Full Text Search](./api/search/GET_FEDERATED_SEARCH_RESULT.md)
  * [Administration](./api/administration/INDEX.md)
    * [Create Project](./api/administration/CREATE_PROJECT.md)
    * [Find A Project](./api/administration/FIND_PROJECT.md)
    * [Update A Project](./api/administration/UPDATE_PROJECT.md)
    * [Re-Analyze A Project](./api/administration/REANALYZE_RPOJECT.md)
    * [Remove A Project](./api/administration/REMOVE_PROJECT.md)
    * [Config Project Analysis](./api/administration/CONFIG_PROJECT_ANALYSIS.md)
    * [Get All Users](./api/administration/GET_ALL_USERS.md)
    * [Add An Admin User](./api/administration/ADD_ADMIN_USER.md)
    * [Remove An Admin User](./api/administration/REMOVE_ADMIN_USER.md)