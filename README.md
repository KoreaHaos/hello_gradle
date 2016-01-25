```
  ___ ___         .__  .__             ________                  .___.__           ._.
 /   |   \   ____ |  | |  |   ____    /  _____/___________     __| _/|  |   ____   | |
/    ~    \_/ __ \|  | |  |  /  _ \  /   \  __\_  __ \__  \   / __ | |  | _/ __ \  | |
\    Y    /\  ___/|  |_|  |_(  <_> ) \    \_\  \  | \// __ \_/ /_/ | |  |_\  ___/   \|
 \___|_  /  \___  >____/____/\____/   \______  /__|  (____  /\____ | |____/\___  >  __
       \/       \/                           \/           \/      \/           \/   \/
```

##### The script:

```bash
# Create a basic directory structure.

mkdir -p src/main/java/hello

# Create HelloWorld Java class.

cat > src/main/java/hello/HelloWorld.java << EOF
package hello;

import org.joda.time.LocalTime;
import java.util.Date;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.TimeZone;

public class HelloWorld {
  public static void main(String[] args) {
    Greeter greeter = new Greeter();

    System.out.println(greeter.sayHello());
    
    LocalTime currentTime = new LocalTime();
    
    System.out.println("Using Joda Time, current local time is: " + currentTime);
    
    
    DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
    Date date = new Date();
    System.out.println("\nUsing Java's Date class, current local date/time is: " + dateFormat.format(date));
    
    Calendar calendar = Calendar.getInstance();
    System.out.println("\nUsing Java's Calendar class' getTime method, current local date/time is: " + dateFormat.format(calendar.getTime()));

    TimeZone timeZone = calendar.getTimeZone();
    System.out.println("\nThe time zone this code is running under is : " + timeZone.getDisplayName());
    
    Fareweller fareweller = new Fareweller();
    System.out.println(fareweller.sayGoodbye());
  }
}
EOF

# Create Greeter Java class.

cat > src/main/java/hello/Greeter.java << EOF
package hello;

public class Greeter {
  
  public String sayHello() {
    return "\nHello Gradle World!\n";
  }
}
EOF

# Create Fareweller Java class.

cat > src/main/java/hello/Fareweller.java << EOF
package hello;

public class Fareweller {
  
  public String sayGoodbye() {
    return "\nGoodbye Hello Gradle World!\n";
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

##### Sources:

* http://gradle.org/
* https://spring.io/guides/gs/gradle/


