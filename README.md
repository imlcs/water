### water 安装
```
kubectl create ns water


helm upgrade --install waterapi \
  --set nameOverride="waterapi" \
  --set containerPort="9371" \
  --set service.port="9371" \
  --set image.repository="noearorg/waterapi" \
  --set image.tag="2.6.1" \
  --set secret."water\.ds\.schema"="water" \
  --set secret."water\.ds\.server"=":3306" \
  --set secret."water\.ds\.username"="" \
  --set secret."water\.ds\.password"="" \
  ./water  -n water 
  
helm upgrade --install watersev \
  --set nameOverride="watersev" \
  --set containerPort="9372" \
  --set service.port="9372" \
  --set image.repository="noearorg/watersev" \
  --set image.tag="2.6.1" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 

helm upgrade --install wateradmin \
  --set nameOverride="wateradmin" \
  --set containerPort="9373" \
  --set service.port="9373" \
  --set image.repository="noearorg/wateradmin" \
  --set image.tag="2.6.1" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 
  
helm upgrade --install waterfaas \
  --set nameOverride="waterfaas" \
  --set containerPort="9374" \
  --set service.port="9374" \
  --set image.repository="noearorg/waterfaas" \
  --set image.tag="2.6.1" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 
  
helm upgrade --install spongeadmin \
  --set nameOverride="spongeadmin" \
  --set containerPort="8171" \
  --set service.port="8171" \
  --set image.repository="noearorg/spongeadmin" \
  --set image.tag="2.1.2" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 
  
helm upgrade --install rockrpc \
  --set nameOverride="rockrpc" \
  --set containerPort="8181" \
  --set service.port="8181" \
  --set image.repository="noearorg/rockrpc" \
  --set image.tag="2.1.2" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 

helm upgrade --install trackapi \
  --set nameOverride="trackapi" \
  --set containerPort="8182" \
  --set service.port="8182" \
  --set image.repository="noearorg/trackapi" \
  --set image.tag="2.1.2" \
  --set secret."solon\.start\.ping"=waterapi:9371 \
  ./water  -n water 
```
