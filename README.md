# CAS
Central Authentication Service

Les fichiers nécessaire sont disponible à l'adresse suivante : [https://github.com/YFanha/CAS](https://github.com/YFanha/CAS)

# Infrastructure

![Infrastructure](assets/infra.png)

# Reverse proxy
J'ai utilisé [Nginx Proxy Manager](https://nginxproxymanager.com/) afin de simplifier la gestion des hôtes.
```yaml
  nginxproxymanager:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    environment:
      DisableIPv6: 'true'
    ports:
      - '80:80'
      - '443:443'
      - '81:81' # Admin Web Portal
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

L'infrastructure étant hébergée chez moi, j'ai redirigé les ports 80 et 443 sur l'hôte afin de gérer ensuite le traffic HTTP/S avec le reverse proxy. Example de la création d'un hôte :
![assets/Pasted image 20250314142702.png](assets/Pasted%20image%2020250314142702.png)

## SSL
![SSL](Pasted%20image%2020250314142856.png)


# Keycloak

![Keycloak 1](assets/Pasted%20image%2020250313142203.png)

![Keycloak 2](assets/Pasted%20image%2020250314115923.png)

![Keycloak 3](assets/Pasted%20image%2020250314115906.png)

![Keycloak 4](assets/Pasted%20image%2020250313142708.png)

# Wordpress
## Ajout du client sur keycloak

![Ajout client Keycloak](assets/Pasted%20image%2020250314140754.png)

## Ajout du plugin

![Ajout plugin](assets/Pasted%20image%2020250306143704.png)

## Configuration du plugin
> **Authorize Endpoint** : https://keycloak.cas.fanha.ch/realms/fanha/protocol/openid-connect/auth  
> **Access Token Endpoint :** https://keycloak.cas.fanha.ch/realms/fanha/protocol/openid-connect/token  

![Configuration plugin](assets/Pasted%20image%2020250314140612.png)

**To find the Client secret, go to the keycloak server WebUI > Client > the client > credentials**

![Client secret](assets/Pasted%20image%2020250314140737.png)

## Tests

![Test 1](assets/Pasted%20image%2020250314135816.png)

![Test 2](assets/Pasted%20image%2020250314140351.png)

# Moodle
