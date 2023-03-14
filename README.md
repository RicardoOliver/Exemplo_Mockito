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

public interface UserDao {
    User getUserById(int userId);
}
