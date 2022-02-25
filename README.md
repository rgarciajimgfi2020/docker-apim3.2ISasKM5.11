# Docker and Docker Compose Resources for WSO2 API Management

This repository contains following Docker resources:

- Alpine, CentOS and Ubuntu based Docker resources for WSO2 API Manager, API Manager Analytics Dashboard and Worker and
Identity Server as Key Manager profiles

- Docker Compose resources for the most common WSO2 API Management deployment patterns

Docker resources for WSO2 API Manager, API Manager Analytics and WSO2 Identity Server as Key Manager
help you build generic Docker images for deploying the corresponding product servers in containerized environments.

Each Docker image includes the Java Development Kit, the relevant product distribution and a collection of utility libraries.
Configurations and non-configuration resources (e.g. binaries such as, third-party libraries, Carbon extensions,
Carbon Applications and security related artifacts such as, Java Keystore files) are designed to be provided via
volume mounts to the containers spawned.

Docker Compose files have been created according to the most common API Management deployment patterns available for allowing users
to quickly evaluate product features along side their co-operate API Management requirements. The Compose files make use of per profile
Docker images of WSO2 API Manager, API Manager Analytics and WSO2 Identity Server as Key Manager, as well as MySQL.

**Change log** from previous v3.1.0.3 release: [View Here](CHANGELOG.md)

URL:
https://medium.com/geekculture/integrating-wso2-apim-api-microgateway-with-wso2-identity-server-2eb3c91caafc

SSO:
https://apim.docs.wso2.com/en/3.2.0/develop/extending-api-manager/saml2-sso/configuring-external-idp-through-identity-server-for-sso/

1.- Configuring Identity Server as IDP for SSO
https://apim.docs.wso2.com/en/3.2.0/develop/extending-api-manager/saml2-sso/configuring-identity-server-as-idp-for-sso/

2.- Configuración de IDP externo a través de Identity Server para SSO 
https://apim.docs.wso2.com/en/3.2.0/develop/extending-api-manager/saml2-sso/configuring-external-idp-through-identity-server-for-sso/


RESULTADO:


Version 4.0 apim y IS 5.11
Problemática con el fallo de login y borrado de permisos:
https://github.com/wso2/carbon-identity-framework/blob/master/components/authentication-framework/org.wso2.carbon.identity.application.authentication.framework/src/main/java/org/wso2/carbon/identity/application/authentication/framework/handler/provisioning/impl/DefaultProvisioningHandler.java

Lineas a tener en cuenta:
            // Whether superadmin login without superadmin role is permitted
            if (deletingRoles
                    .contains(realm.getRealmConfiguration().getAdminRoleName())) {
                if (log.isDebugEnabled()) {
                    log.debug("Federated user doesn't have super admin role. Unable to sync roles, since" +
                            " super admin role cannot be unassigned from super admin user");
                }
                throw new FrameworkException(
                        "Federated user which having same username to super admin username of local IdP," +
                                " trying login without having super admin role assigned");
            }
        }
    }
