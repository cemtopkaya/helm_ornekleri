# helm_ornekleri

WSL üstünde bir ubuntu'ya docker-ce, minikube, helm kurmak için
https://gist.github.com/cemtopkaya/02ffd0a76e1fa9b878497b272da98d97

Helm Chart paket havuzunu konteyner olarak çalıştıralım:

```bash
docker run --rm -it \
  -p 8080:8080 \
  -e DEBUG=1 \
  -e STORAGE=local \
  -e STORAGE_LOCAL_ROOTDIR=/charts \
  -v $(pwd)/charts:/charts \
  ghcr.io/helm/chartmuseum:v0.13.1
```

![image](https://user-images.githubusercontent.com/261946/143963256-960f511e-b3ff-4c74-b010-3e97698404e7.png)

```bash
helm repo list
helm repo add yerel http://localhost:8080
helm repo update
helm search repo hede
helm repo remove yerel
```

## Bağımlılık Kontrolü Yapıyoruz
Bağımlılıklar, belirtildikleri adreslerde yoksa aşağıdaki gibi hata verir:

![image](https://user-images.githubusercontent.com/261946/143964194-7f6b53c2-dd33-48f5-815e-e7f1d92d6b59.png)

Başarılı ve başarısız bağımlılıklar olsun. https://charts.helm.sh/stable/ Repo listemizde tanımlı olmadığı için her `helm dependency update <paket-adı>` 
çalıştığında charts.helm.sh adresinden verileri çekip sonra ilgili bağımlılığı arıyor.

![image](https://user-images.githubusercontent.com/261946/143966648-c3ae708b-439b-4746-b72f-2c534dcfb046.png)

