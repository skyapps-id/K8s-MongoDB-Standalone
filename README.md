# Deployment MongoDB to Kubernetes

🚢[Docker Image](https://hub.docker.com/_/mongo)

### Running On Premise 
- Ubuntu 20.04 LTS
- Storage Class Rook Ceph Block

### Specification My Cluster
- Master node vCPU 2 Memory 8Gb
- Worker node1 vCPU 2 Memory 4Gb
- Worker node2 vCPU 2 Memory 4Gb
- Worker node3 vCPU 2 Memory 4Gb

### Installation
1. Clone this project.
    ```sh
    $ git clone https://github.com/skyapps-id/K8s-MongoDB-Standalone.git 
    ```

2. Create the Secret resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ cd  K8s-MongoDB-Standalone/
    $ kubectl apply -f secret-mongodb.yml
    ```
     - NOTE Secrets data are stored as Base64 encoded strings. command : ```$ echo -n 'example' | base64 ``` example mongo user ``admindb`` password is ``adminpassword``

4. Creating a Presistance Volume Claim resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f persistent-volume-claim-mongodb.yaml
    ```

5. Deployment MongoDB resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f deployment-mongodb.yaml
    ```

6. Creating a Service resource in your Kubernetes cluster by using the kubectl apply command.
    ```sh
    $ kubectl apply -f service-mongodb.yaml
    ```

7. Testing MongoDB Service.
    ```sh
    $ kubectl get pods
    NAME                     READY   STATUS    RESTARTS   AGE
    mongo-6f5b88f7f6-v94ks   1/1     Running   0          14m

    $ kubectl exec -it mongo-6f5b88f7f6-v94ks -- mongo
    MongoDB shell version v4.4.4
    connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
    Implicit session: session { "id" : UUID("4d114876-9265-4649-b154-eeb2ce696859") }
    MongoDB server version: 4.4.4
    > use admin
    switched to db admin
    > db.auth('admindb','adminpassword')
    1
    > show tables
    system.users
    system.version
    >
    ```

### Licence

This work is under [MIT](LICENCE) licence.