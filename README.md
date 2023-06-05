# PROCESSO-SELETIVO-Chuteira-CRUD

public class Chuteira { 

private int id;    
private String marca;   
private String modelo;   
private double preco;   

// Construtores, getters e setters   

// Método para exibir informações da chuteira   

public void exibirInformacoes() {     

System.out.println("ID: " + id);     
System.out.println("Marca: " + marca);     
System.out.println("Modelo: " + modelo);    
System.out.println("Preço: " + preco);    
}

}

-----------------------------------

import java.util.List;

public interface ChuteiraDAO {

 void salvar(Chuteira chuteira);
 Chuteira buscarPorId(int id);
 List<Chuteira> listar();  
 void atualizar(Chuteira chuteira);
 void deletar(int id);
}
  
----------------------------------
  
 import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class ChuteiraDAOImpl implements ChuteiraDAO {
  private Map<Integer, Chuteira> chuteiras;

  public ChuteiraDAOImpl() {
        chuteiras = new HashMap<>();
    }

 @Override
  public void salvar(Chuteira chuteira) {
      chuteiras.put(chuteira.getId(), chuteira);
    }

 @Override
 public Chuteira buscarPorId(int id) {
        return chuteiras.get(id);
    }
  
  @Override
  public List<Chuteira> listar() {
        return new ArrayList<>(chuteiras.values());
    }
  @Override
   public void atualizar(Chuteira chuteira) {
        chuteiras.put(chuteira.getId(), chuteira);
    }

@Override
 public void deletar(int id) {
       chuteiras.remove(id);
    }
}
--------------------------------------------------------
  import java.util.List;

public class Main {
    public static void main(String[] args) {
        ChuteiraDAO chuteiraDAO = new ChuteiraDAOImpl();
        // Criar e salvar uma nova chuteira
        Chuteira chuteira1 = new Chuteira();
        chuteira1.setId(1);
        chuteira1.setMarca("Nike");
        chuteira1.setModelo("Mercurial");
        chuteira1.setPreco(299.99);
        chuteiraDAO.salvar(chuteira1);
  
        // Buscar e exibir informações de uma chuteira por ID
       Chuteira chuteira2 = chuteiraDAO.buscarPorId(1);
        if (chuteira2 != null) {
          chuteira2.exibirInformacoes();
        }

       // Atualizar informações de uma chuteira
       if (chuteira2 != null) {
            chuteira2.setPreco(329.99);
           chuteiraDAO.atualizar(chuteira2);
        }

        // Listar todas as chuteiras
        List<Chuteira> chuteiras = chuteiraDAO.listar();
        for (Chuteira chuteira : chuteiras) {
            chuteira.exibirInformacoes();
            System.out.println();
        }
        // Deletar uma chuteira por ID
        chuteira
