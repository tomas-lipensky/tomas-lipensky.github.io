Automatizace nasazování databázových změn. Verzování změn, nasazování změn spolu s verzí aplikace.

#### CMD

liquibase --version  
liquibase --secure-parsing=false --defaultsFile=liquibase.docker.properties update --changelog-file db.changelog-master.xml  

#### JAVA client

`%%java -jar liquibase.jar --driver com.mysql.jdbc.Driver --classpath=mysql-connector-java-5.1.43-bin.jar --username=USR --password=PWD --url=jdbc://localhost/lb --changeLogFile=xmlsample/changelog.xml update%%` ... update operace nad mysql  
`%%java -jar liquibase.jar --driver oracle.jdbc.driver.OracleDriver --classpath=ojdbc7.jar  --username=USR --password=PWD --url=jdbc:oracle:thin:@IP:1521/DB --changeLogFile=xmlsample/changelog.xml rollbackCount 1%%` ... rollback operace o jeden krok nad Oracle databází  

=== ChangeSet format ===

```
<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
  xmlns:xsi="http://www.wš.org/2001XMLSchemaInstance"
  xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.wš.org/2001XMLSchemaInstance http://www.liquibase.org/xml/ns/dbchangelog-ext">
  <include file="db/changeset1.xml"/>
  <include file="db/changeset1.xml"/>
</databaseChangeLog>
```

```
<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
  xmlns:xsi="http://www.wš.org/2001XMLSchemaInstance"
  xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.wš.org/2001XMLSchemaInstance http://www.liquibase.org/xml/ns/dbchangelog-ext">
  <changeSet id=0 author="tom">
    <createTable tableName="tabulka1">
      <column name="id" type="int">
        <constrains primaryKey="true" nullable="false" />
      </column>
    </createTable>
  </changeSet>
</databaseChangeLog>
```
