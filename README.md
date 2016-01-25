```
  ___ ___         .__  .__             ________                  .___.__           ._.
 /   |   \   ____ |  | |  |   ____    /  _____/___________     __| _/|  |   ____   | |
/    ~    \_/ __ \|  | |  |  /  _ \  /   \  __\_  __ \__  \   / __ | |  | _/ __ \  | |
\    Y    /\  ___/|  |_|  |_(  <_> ) \    \_\  \  | \// __ \_/ /_/ | |  |_\  ___/   \|
 \___|_  /  \___  >____/____/\____/   \______  /__|  (____  /\____ | |____/\___  >  __
       \/       \/                           \/           \/      \/           \/   \/
```

### The script:

```bash
# Create a basic directory structure.

mkdir -p src/main/java/hello

# Create HelloWorld Java class.

cat > src/main/java/hello/HelloWorld.java << EOF
package hello;

import org.joda.time.LocalTime;

public class HelloWorld {
  public static void main(String[] args) {
    LocalTime currentTime = new LocalTime();
    System.out.println("The current local time is: " + currentTime);

    Greeter greeter = new Greeter();
    System.out.println(greeter.sayHello());
  }
}
EOF

# Create Greeter Java class.

cat > src/main/java/hello/Greeter.java << EOF
package hello;

public class Greeter {
  public String sayHello() {
    return "Hello world!";
  }
}
EOF

# Create build.gradle file.

cat > build.gradle << EOF
apply plugin: 'java'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'

// tag::repositories[]
repositories {
    mavenCentral()
}
// end::repositories[]

// tag::jar[]
jar {
    baseName = 'gs-gradle'
    version =  '0.1.0'
}
// end::jar[]

// tag::dependencies[]
sourceCompatibility = 1.7
targetCompatibility = 1.7

dependencies {
    compile "joda-time:joda-time:2.2"
}
// end::dependencies[]

// tag::wrapper[]
task wrapper(type: Wrapper) {
    gradleVersion = '2.3'
}
// end::wrapper[]
EOF

# Install gradle with no prompt.

sudo apt-get -y install gradle

# Build the gradle wrapper.

gradle wrapper

# Run the program.

./gradlew run

# That's it.
```
