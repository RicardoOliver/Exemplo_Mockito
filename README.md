# Exemplo Mockito

<p>Mockito: uma das ferramentas de mock mais populares em Java. Permite a criação de objetos simulados, chamados de "mocks", que podem ser usados para testar a interação entre componentes.<p>

  
  Suponha que temos uma classe UserService que tem um método getUserById que retorna um objeto User com base no ID fornecido. Queremos testar essa classe usando   Mockito para simular o objeto UserDao que é usado internamente pelo UserService.
  
  ```java
  public class UserService {
    private UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }

    public User getUserById(int userId) {
        return userDao.getUserById(userId);
    }
}
`````java
  
public interface UserDao {
    User getUserById(int userId);
}
  
Aqui está um exemplo de teste de unidade usando Mockito para simular o objeto UserDao:
 ```java
  import static org.mockito.Mockito.*;
import org.junit.*;
import org.mockito.*;

public class UserServiceTest {
    @Mock
    private UserDao userDao;

    @InjectMocks
    private UserService userService;

    @Before
    public void setUp() {
        MockitoAnnotations.initMocks(this);
    }

    @Test
    public void testGetUserById() {
        // Criação de um objeto User fictício
        User fakeUser = new User();
        fakeUser.setId(1);
        fakeUser.setName("John Doe");

        // Configuração do comportamento simulado do objeto UserDao
        when(userDao.getUserById(1)).thenReturn(fakeUser);

        // Chama o método getUserById do objeto UserService
        User user = userService.getUserById(1);

        // Verifica se o objeto UserDao foi chamado corretamente
        verify(userDao).getUserById(1);

        // Verifica se o usuário retornado é igual ao usuário fictício criado acima
        assertEquals(user, fakeUser);
    }
}
