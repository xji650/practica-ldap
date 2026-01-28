# Imatge base de OpenLDAP, bona pràctica fixar la versió
# TLS/SSL es genera automàticament per la imatge osixia/openldap
FROM osixia/openldap:1.5.0

# Configuració variables d'entorn $BASE i $DC
ENV LDAP_ORGANISATION="UdL"
ENV LDAP_DOMAIN="amsa.udl.cat"
ENV LDAP_BASE_DN="dc=amsa,dc=udl,dc=cat"

# Pasword de l'administrador (admin)
ENV LDAP_ADMIN_PASSWORD="adminpassword"
ENV LDAP_CONFIG_PASSWORD="configpassword"

# Copiem el nostre fitxer LDIF a la carpeta d'inici
# La imatge osixia executa tot el que hi ha en aquesta carpeta en arrencar
COPY bootstrap.ldif /container/service/slapd/assets/config/bootstrap/ldif/50-bootstrap.ldif

# Exposem els ports LDAP i LDAPS (opcional, ja que la imatge ja ho fa)
EXPOSE 389 636