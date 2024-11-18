```java
@Service
public class UserService {
    private final UserRepository userRepository;
    private final EmailService emailService;

    // Bean 이름을 simpleUserService로 지정
    @Bean("simpleUserService")
    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
        this.emailService = null;
    }

    // Bean 이름을 fullUserService로 지정
    @Primary
    @Bean("fullUserService")
    @Autowired  
    public UserService(UserRepository userRepository, EmailService emailService) {
        this.userRepository = userRepository;
        this.emailService = emailService;
    }
}

@Controller
public class UserController {
    // Primary가 있는 fullUserService가 주입됨
    @Autowired
    private UserService userService;
    
    // simpleUserService Bean이 주입됨
    @Autowired
    @Qualifier("simpleUserService")  
    private UserService simpleService;
    
    // fullUserService Bean이 주입됨
    @Autowired
    @Qualifier("fullUserService")
    private UserService fullService;
}
```

@Bean 어노테이션으로 각각의 생성자에 이름을 붙여서 구분할 수 있다.

git commit 되려나
