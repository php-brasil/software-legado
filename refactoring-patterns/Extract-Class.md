__Extração de Classe__

O refactoring de extração de classe tem como motivação o momento em que você identifica em uma classe lidando com comportamentos que, apesar de serem importantes para ela(ou não) são comportamentos que podem ser isolados e assim, reduzir a complexidade da classe de origem.

Lembrando as sabias palavras do Martin Fowler: não faz sentido refactoring num codigo em um programa tão curto, afinal, o benefício não é claro, ou, segundo o dicionario novilingua, é _desbenefício_.

```
Class Pessoa{
 private $endereco = ['rua'=>null,'numero'=>null];
 private $nome;
 
 public function setEndereco($rua, $numero)
 {
     $this->endereco['rua']    = $rua;
     $this->endereco['numero'] = $numero;
 }
 
 public function setNome($nome)
 {
     $this->nome = $nome;
 } 
}
```

Apesar de estar claro o interesse da classe pessoa em ter informações sobre o endereço, também é claro que se trata de:

* Existe um conjunto de dados dentro do conjunto de dados que Pessoa deve administrar

* Existe uma responsabilidade em administrar(set,get) esse conjunto de dados.

* O conjunto de dados Endereço pode ser de interesse de outras classes.

Então o que fazemos é dar mais granularidade a nossa classe.

```
// criamos uma classe que assume a responsabilidade de lidar com o conjunto de dados chamado Endereço.

Class Endereco{
    private $rua;
    private $numero;
    
    public function setRua($rua)
    {
        $this->rua = $rua;
    }
    
    public function setNumero($numero){
        $this->numero - $numero;
    }
}
```

E passamos para o refactoring da classe principal

```
Class Pessoa{
 // alteramos a propriedade endereco que deixa de ser uma estrutura de dados
 private $endereco;
 private $nome;
 
 // e o método que deixa de receber primitivos para receber o tipo Endereco
 public function setEndereco(Endereco $endereco)
 {
     $this->endereco = $endereco
 }
 
 public function setNome($nome)
 {
     $this->nome = $nome;
 } 
}
```

O resultado é que o software passa a ter mais granularidade e com isso maior reaproveitamento. Outro benefício é que a responsabilidade da classe pessoa passou a ser limitada a lidar com pessoa e não com os subtipos que o projetista/designer definiu que deveriam compor a classe Pessoa.

