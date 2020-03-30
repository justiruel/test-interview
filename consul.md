## Install Consul
- donwnload consul exe daftarkan di path environtment variable
- tes dengan ketik consul di cli
## Register Service
- buat order1.json
```
{
  "ID": "order1",
  "Name": "order",
  "Tags": [
    "v1"
  ],
  "Address": "127.0.0.1",
  "Port": 5000,
  
  "Check": {
    "DeregisterCriticalServiceAfter": "90m",
     "id": "be-http-check",
	 "name": "HTTP API on port 5000",
	 "http": "http://127.0.0.1:5000/halo",
	 "interval": "5s",
	 "timeout": "1s"
  }
}
```
- buat order2.json
```
{
  "ID": "order2",
  "Name": "order",
  "Tags": [
    "v1"
  ],
  "Address": "127.0.0.1",
  "Port": 5001,
  
  "Check": {
    "DeregisterCriticalServiceAfter": "90m",
     "id": "be-http-check",
	 "name": "HTTP API on port 5001",
	 "http": "http://127.0.0.1:5001/halo",
	 "interval": "5s",
	 "timeout": "1s"
  }
}
```
- jalankan
```
$ curl \
    --request PUT \
    --data @order1.json \
    http://127.0.0.1:8500/v1/agent/service/register?replace-existing-checks=true	
```
- jalankan
```
$ curl \
    --request PUT \
    --data @payload.json \
    http://127.0.0.1:8500/v1/agent/service/register?replace-existing-checks=true
```
## Jalankan Consul
- ketik 
```
consul agent -dev -ui -datacenter zone1 -node host1
```
- coba akses http://localhost:8500/ui/

## Penggunaan
- consul client => D:\PROJECT\RESEARCH\NODEJS\consul-learn
- port 5000 dan 5001 => D:\PROJECT\RESEARCH\NODEJS\simple-express

## Daftar Pustaka
- https://www.npmjs.com/package/consul#kv-get
- https://www.npmjs.com/package/consulite/v/1.2.0?activeTab=readme
- https://thenewstack.io/implementing-service-discovery-of-microservices-with-consul/
- https://www.consul.io/api/agent/service.html
