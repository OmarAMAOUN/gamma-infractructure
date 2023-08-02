# generate user certificates:
kubectl -n kafka get secret infocentre-user -o jsonpath='{.data.user\.crt}' | base64 -d > user.crt
kubectl -n kafka get secret infocentre-user -o jsonpath='{.data.user\.key}' | base64 -d > user.key
kubectl -n kafka get secret gamma-cluster-cluster-ca-cert -o jsonpath='{.data.ca\.crt}' | base64 -d > ca.crt

keytool -import -trustcacerts -file ca.crt -keystore truststore.jks -storepass 123456
openssl pkcs12 -export -in user.crt -inkey user.key -name infocentre-user -password pass:123456 -out user.jks
