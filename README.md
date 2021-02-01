# buscaCep
Uma função para o google planilhas que busca o CEP por API e traz dentro da planilha, Logradouro, Bairro, Cidade, Estado e DDD.


### É uma função bem simples e objetivo é ajudar pessoas que trabalham com tabelas de Cep e precisam ficar copiando e colando informações em uma planilha. 

## Vou colocar aqui um passo a passo para facilitar a vida de quem não programa.

- 1º Faça uma cópia da minha planilha.([Planilha](http://bit.ly/busca_CEP))
- 2º Na barra superior do Google Planilhas clique em Ferramentas > Editor de Script.
- 3º Copie o código abaixo na tela que irá abrir.
- 4º Dê as permissões necessárias. 
- 5º Copie um CEP válido, com oito digitos e sem hifen no formato texto simples. 
- 6º A essa altura existe um menu na barra superior chamado 'Busca CEP' clique nele e pronto a API era trazer para sua planilha as informações de  Logradouro, Bairro, Cidade, Estado e DDD

```javascript
function onOpen () 
{
  var ui = SpreadsheetApp.getUi ();
  ui.createMenu ('Buscar CEP')
      .addItem ('Buscar CEP', 'myFunction')
      .addToUi ();
}
```




```javascript
function myFunction () 

{
   var sheet = SpreadsheetApp.getActiveSheet ();
   var row = 5;
   var col = 8;
   var data = sheet.getRange (row, col) .getValue ();

   Logger.log(data)


//buscando a página da API

var cep = (data)

var url = ("viacep.com.br/ws/" + cep + "/json/unicode");
var response = UrlFetchApp.fetch(url, {'muteHttpExceptions': true});
var json = response.getContentText();
var data = JSON.parse(json);

//Imprimindo os dados
var lastRow=sheet.getLastRow()+1;
var i=0;
sheet.getRange(lastRow+i, 1).setValue(data.cep);
sheet.getRange(lastRow+i, 2).setValue(data.logradouro);
sheet.getRange(lastRow+i, 3).setValue(data.bairro);
sheet.getRange(lastRow+i, 4).setValue(data.localidade);
sheet.getRange(lastRow+i, 5).setValue(data.uf);
sheet.getRange(lastRow+i, 6).setValue(data.ddd);

}
```
