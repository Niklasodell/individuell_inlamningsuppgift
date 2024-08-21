# Vad jag har gjort i gruppuppgiften

Gjorde en kompleterande uppgift för gruppuppgiften då jag ej hjälpte till med gruppuppgiften.


# 1
``` java

public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .csrf(csrf -> csrf.ignoringRequestMatchers("/register", "/delete"))
                .authorizeHttpRequests(authorizeRequests ->
                        authorizeRequests
                                .requestMatchers( "/login", "/logout" ).permitAll()
                                .requestMatchers("/register").hasRole("ADMIN")
                                .requestMatchers("/homepage").permitAll()
                                .requestMatchers("/admin/**").hasRole("ADMIN")
                                .requestMatchers( "/users", "/delete" ).hasRole( "ADMIN" )
                                .anyRequest().authenticated()
                )
                .formLogin(formLogin ->
                        formLogin
                                .loginPage("/login")
                                .defaultSuccessUrl("/homepage", true)
                                .failureUrl("/login?error=true")
                                .permitAll()
                )
                .oauth2Login(oauth2Login ->
                        oauth2Login
                                .loginPage("/login")
                                .defaultSuccessUrl("/login", true)
                                .failureUrl("/login?error=true")
                )
                .logout(logout -> logout
                        .logoutUrl("/perform_logout"  )
                        .logoutSuccessUrl( "/login" )
                        .permitAll());

        return http.build();
    }
    
```


# 2 

"public": Metoder och variabler är tillgängliga för alla delar av programmet. 
"private": Metoder och variabler är endast tillgängliga inom den egna klassen.


# 3

"void": Metoden returnerar inget värde.
typ eller klass: Metoden returnerar ett värde av den angivna typen eller klassen.


# 4

I Java bör metodnamn följa "camelCase"-konventionen, 
där det första ordet är i gemener och varje efterföljande ord börjar med en versal. 
Exempel: `calculateTotalAmount`, `getUserName`.


# 5 

Om det inte står något mellan parenteserna () efter metodnamnet innebär det att metoden inte tar några argument.


# 6

Det som skickas med till metoden mellan parenteserna kallas "argument" eller "parameter".


# 7

``` java

public int add(int a, int b) {
    return a + b;
}

```

# 8

``` java

public class ExampleAdd {
    public int add(int a, int b) {
        return a + b;
    }

    public void callingAdd() {
        int result = add(5, 3);
        System.out.println("Resultatet är: " + result);
    }
}
    
```

# 9

``` java

public class HakansClass {
    private String name;
    private int age;

    public tomKonstruktor() {
        
        this.name = "Unknown"; // Sätter standardvärde för name
        this.age = 0;          // Sätter standardvärde för age
    }

    public void displayTomKonstruktor() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

```

# 10

``` java

public class Main {
    public static void main(String[] args) {
        // 1) Skapande av en primitiv typ med ett värde
        int number = 42; // 'number' är en primitiv typ (int) med värdet 42

        // 2) Skapande av ett objekt (en instans av en klass)
        Person person = new Person(); // 'person' är ett objekt av klassen Person
    }
}

// Klassdefinition för exemplet
class Person {
    // Tom klass
}

```


# 11

I Java ska metodnamn börja med ett verb, 
som tydligt beskriver vad metoden gör, 
och använda camelCase (t.ex. `calculateTotal()`). 
Metodnamn bör vara beskrivande för att göra koden lättläst och förståelig.

I Spring, med @Bean-annoterade metoder, 
är det vanligt att namnge metoden efter den typ den returnerar 
(t.ex. `hakansClass()` för att returnera en instans av `HakansClass`).


# 12

`@Override` används för att indikera att en metod i en 
subklass överskrider en metod i en superklass eller implementerar en metod från ett interface.

Det hjälper till att förhindra fel och gör koden tydligare.

# 13

``` java

public class MyCustomAuthenticationProvider extends DaoAuthenticationProvider {

    public MyCustomAuthenticationProvider() {
    }

    @Override
    public Authentication authenticate(Authentication auth) throws AuthenticationException {'
        return super.authenticate(auth);
    }
}

```

# 14

`PasswordEncoder`-bean i Spring Security används för att hasha lösenord vid registrering, 
så att de lagras säkert i databasen. 

Vid inloggning används den för att verifiera det angivna lösenordet genom att jämföra det med det hashede lösenordet som finns i databasen. 

Detta säkerställer att lösenord hanteras säkert både vid lagring och autentisering.


# 15

```xml

<configuration>

    <!-- Console Appender (valfri) -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- File Appender -->
    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>application.log</file>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- Rolling File Appender -->
    <appender name="ROLLING" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>daily.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>daily-%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- Logger for the package -->
    <logger name="se.sprinto.hakan.securityapp" level="debug">
        <appender-ref ref="ROLLING"/>
    </logger>

    <!-- Root Logger -->
    <root level="info">
        <appender-ref ref="FILE"/>
        <appender-ref ref="CONSOLE"/>
    </root>

</configuration>

```


# 16

- 200 OK: Begäran har lyckats, och svaret innehåller den begärda resursen.
- 401 Unauthorized: Begäran kräver autentisering; användaren måste logga in för att få åtkomst.
- 403 Forbidden: Servern förstår begäran men vägrar att utföra den; användaren har inte tillåtelse.
- 404 Not Found: Den begärda resursen kunde inte hittas på servern.
