//Pedido pessoal, esse código so deverá ser utilizado para estudo e tirar duvidas.
//Qualquer edição feita nele não deve ser salva a menos que necessário.
//link do vídeo original:https://www.youtube.com/watch?v=Gowt3ii58gQ&t=1375s.
import 'package:flutter/material.dart';
void main(){
 runApp(MaterialApp(
  home: Home(), 
 ));  
}
class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {

  String infoText= "informe seus dados";

  TextEditingController weightcontroller = TextEditingController();
  TextEditingController heightcontroller = TextEditingController();  

  Widget buildTextfield(String label, TextEditingController c){
    return TextField(
              decoration: InputDecoration(
                labelText: label, labelStyle: TextStyle(color: Colors.green, fontSize: 20),
                border: OutlineInputBorder()
              ),
              style: TextStyle(color: Colors.green, fontSize: 25),
              keyboardType: TextInputType.number,
              controller: c,
      );      
    }
    void _resetFields(){
      setState(() {      
      weightcontroller.text = "";
      heightcontroller.text = "";
      infoText = "Informe seus dados";
      });
    }

    void _calculate(){
      double weight = double.parse(weightcontroller.text);
      double height = double.parse(heightcontroller.text) / 100;
      double imc = weight / (height * height);
       setState(() {         
      if (imc < 17) {
        infoText = "Muito abaixo do peso (${imc.toStringAsPrecision(4)})";
      }else if(imc >=17 && imc<=18.49){
        infoText = "Abaixo do peso (${imc.toStringAsPrecision(4)})";
      }else if(imc >=18.50 && imc<=24.99){
        infoText = "Peso ideal ou normal(${imc.toStringAsPrecision(4)})";
      }else if(imc >=25 && imc<=29.99){
        infoText = "Acima do peso (${imc.toStringAsPrecision(4)})";
      }else if(imc >=30 && imc<=34.99){
        infoText = "Obesidade (${imc.toStringAsPrecision(4)})";
      }else if(imc >=35 && imc<=39.99){
        infoText = "Obesidade II (severa) (${imc.toStringAsPrecision(4)})";
      }else if(imc >40) {
        infoText = "Obesidade III (mórbida) (${imc.toStringAsPrecision(4)})";          
      }
       });
    }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.green,
        title: Text("Calculadora IMC"),
        centerTitle: true,
        actions: <Widget>[
          IconButton(icon: Icon(Icons.refresh),
          onPressed: (){_resetFields();},)
        ],
      ),
      body: SingleChildScrollView(
        padding: EdgeInsets.all(10.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Icon(Icons.person_outline, size: 170, color: Colors.green,),
          buildTextfield("Peso", weightcontroller),
          Divider(),
          buildTextfield("Altura", heightcontroller),
          Padding(
            padding: const EdgeInsets.only(top: 10.0),
            child: Container(
              height: 50.0,
              child: RaisedButton(
                child: Text("Verificar", style: TextStyle(color: Colors.white, fontSize: 25.0),),
                onPressed: (){
                  _calculate();
                },
                color: Colors.green,
              ),
            ),
          ),
          Padding(
            padding: const EdgeInsets.only(top: 10.0),
            child: Text(infoText, style: TextStyle(color: Colors.green, fontSize: 25.0),
            textAlign: TextAlign.center,),
          )
          ],
        ),
      )

    );
  }
}
