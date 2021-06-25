    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-antrun-plugin</artifactId>
        <version>3.0.0</version>
        <executions>
            <execution>
                <id>project-metadata</id>
                <phase>validate</phase>
                <configuration>
                    <target name = "build-metadata">
                        <property name = "project.groupId" value = "${project.groupId}"/>
                        <property name = "project.artifactId" value = "${project.artifactId}"/>
                        <property name = "project.version" value = "${project.version}"/>
                        <property name = "project.name" value = "${project.name}"/>
                        <condition property = "source.exists">
                            <available file = "src" type = "dir"/>
                        </condition>
                        <taskdef resource = "net/sf/antcontrib/antcontrib.properties" classpathref = "maven.plugin.classpath"/>
                        <if>
                            <equals arg1 = "${source.exists}" arg2 = "true"/>
                            <then>
                                <echo file = "src/main/java/project.properties">
                                    project-name = ${project.name}${line.separator}project-version = ${project.version}${line.separator}project-group-id = ${project.groupId}${line.separator}project-artifact-id = ${project.artifactId}
                                </echo>
                            </then>
                            <else>
                                <echo file = "${project.basedir}/project.properties">
                                    project-name = ${project.name}${line.separator}project-version = ${project.version}${line.separator}project-group-id = ${project.groupId}${line.separator}project-artifact-id = ${project.artifactId}
                                </echo>
                            </else>
                        </if>
                    </target>
                </configuration>
                <goals>
                    <goal>run</goal>
                </goals>
            </execution>
        </executions>
        <dependencies>
            <dependency>
                <groupId>ant-contrib</groupId>
                <artifactId>ant-contrib</artifactId>
                <version>20020829</version>
            </dependency>
        </dependencies>
    </plugin>
