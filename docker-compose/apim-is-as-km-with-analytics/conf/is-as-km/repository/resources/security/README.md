keytool -delete -trustcacerts -alias wso2carbon -keystore client-truststore.jks
rm -rf wso2carbon.jks
keytool -genkey -alias wso2carbon -keyalg RSA -keysize 2048 -validity 3650 -keystore wso2carbon.jks -dname "CN=*.wso2.inetum,OU=EI,O=WSO2,L=Sevilla,S=ANDALUCIA,C=ES" -ext "SAN=IP:51.124.232.89,DNS:wso2iskm.wso2.inetum" -storepass wso2carbon -keypass wso2carbon -noprompt
keytool -export -alias wso2carbon -keystore wso2carbon.jks -file pkn.pem
keytool -import -trustcacerts -alias wso2carbon -file pkn.pem -keystore client-truststore.jks -storepass wso2carbon