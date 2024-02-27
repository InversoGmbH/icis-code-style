# ICIS Code Style
Hier finden sich Formattierungsregeln bzw. Vorlagen für diverse Programmiersprachen und Tools.

## Java
### Generelle Vorgaben
- Einrückung mit einem Tabulator pro Einrückungsebene
- geschweifte Klammern entweder auf neuer oder gleicher Zeile
- einheitliche Formattierung innerhalb des Projekts
- Imports alphabetisch sortiert
- Import ins zwei Gruppen: statische und nicht-statische getrennt
- statische Import nach nicht-statischen Imports
- abschließender Zeilenumbruch (new line at end of file)
- kein trailing whitespace

### Formatter für Eclipse

Die Eclipse Formatter können wahlweise direkt in Eclipse importiert oder bei Builds-Tools wie Maven eingebunden werden.

Den Formatter gibt es in den folgenden Ausführungen:

- `eclipse-formatter-same-line.xml`: geschweifte Klammern auf einer Zeile

#### Integration mit Maven mit [spotless-maven-plugin](https://github.com/diffplug/spotless/tree/main/plugin-maven#eclipse-jdt)

```xml
	<plugin>
		<groupId>com.diffplug.spotless</groupId>
		<artifactId>spotless-maven-plugin</artifactId>
		<version>2.43.0</version>
		<executions>
			<execution>
				<goals>
					<goal>check</goal>
				</goals>
				<phase>process-sources</phase>
			</execution>
		</executions>
		<configuration>
			<formats>
				<!-- you can define as many formats as you want, each is independent -->
				<format>
					<!-- define the files to apply to -->
					<includes>
						<include>.gitignore</include>
						<include>pom.xml</include>
						<includes>*.yml</includes>
					</includes>
					<!-- define the steps to apply to those files -->
					<trimTrailingWhitespace />
					<endWithNewline />
					<indent>
						<tabs>true</tabs>
					</indent>
				</format>
			</formats>
			<!-- define a language-specific format -->
			<java>
				<eclipse>
					<version>4.30</version> <!-- siehe https://central.sonatype.com/artifact/org.eclipse.platform/org.eclipse.platform -->
					<file>https://raw.githubusercontent.com/InversoGmbH/icis-code-style/main/java/eclipse-formatter-same-line.xml</file>
				</eclipse>
				<removeUnusedImports />
				<importOrder>
					<order>,\#</order>
				</importOrder>
				<trimTrailingWhitespace />
				<endWithNewline />
			</java>
		</configuration>
	</plugin>
```
