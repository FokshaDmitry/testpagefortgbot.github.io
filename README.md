<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Telegram WebApps API</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script> <!--Подключаем скрипт от телеграм-->
</head>

<body>
    <div id="usercard">
        <!--Карта профиля, человека, который к нам обратился-->
    </div>
    <p>Just texxXXXt</p> <!--Просто текст для проверки-->
    <p class="hint">Some little hint</p> <!--Просто текст-подсказка для проверки-->
    <button id="btn" class="button">Show/Hide Main Button</button> <!--Кнопка, чтобы скрыть / показать основную кнопку-->
    <button id="btnED" class="button">Enable/Disable Main Button</button> <!--Кнопка, чтобы сделать кнопку активной/неактивной-->
</body>

<script>
   let tg = window.Telegram.WebApp; //получаем объект webapp телеграма

   tg.expand(); //расширяем на все окно

   //tg.MainButton.text = "Changed Text"; //изменяем текст кнопки
   //tg.MainButton.setText("Changed Text1"); //изменяем текст кнопки иначе
   //tg.MainButton.textColor = "#F55353"; //изменяем цвет текста кнопки
   //tg.MainButton.color = "#143F6B"; //изменяем цвет бэкграунда кнопки
   //tg.MainButton.setParams({"color": "#143F6B"}); //так изменяются все параметры
    tg.sendData('[{"Country": "Name","Tariffs": [{"Name": "Random","Quantity": 2,"Price": 40},{"Name": "Fixed","Quantity": 2,"Price": 40}]},{"Country": "Name","Tariffs": [{"Name": "Random","Quantity": 2,"Price": 40},{"Name": "Fixed","Quantity": 2,"Price": 40}]}]');
   let btn = document.getElementById("btn"); //получаем кнопку скрыть/показать

   btn.addEventListener('click', function(){ //вешаем событие на нажатие html-кнопки
      if (tg.MainButton.isVisible){ //если кнопка показана
         tg.MainButton.hide() //скрываем кнопку
      }
      else{ //иначе
         tg.MainButton.show() //показываем
      }
   });

   let btnED = document.getElementById("btnED"); //получаем кнопку активировать/деактивировать
   btnED.addEventListener('click', function(){ //вешаем событие на нажатие html-кнопки
      if (tg.MainButton.isActive){ //если кнопка показана
         tg.MainButton.setParams({"color": "#E0FFFF"}); //меняем цвет
         tg.MainButton.disable() //скрываем кнопку
      }
      else{ //иначе
         tg.MainButton.setParams({"color": "#143F6B"}); //меняем цвет
         tg.MainButton.enable() //показываем
      }
   });

   Telegram.WebApp.onEvent('mainButtonClicked', function(){
      tg.sendData('[{"Country": "Name","Tariffs": [{"Name": "Random","Quantity": 2,"Price": 40},{"Name": "Fixed","Quantity": 2,"Price": 40}]},{"Country": "Name","Tariffs": [{"Name": "Random","Quantity": 2,"Price": 40},{"Name": "Fixed","Quantity": 2,"Price": 40}]}]');
      //при клике на основную кнопку отправляем данные в строковом виде
   });


   let usercard = document.getElementById("usercard"); //получаем блок usercard
   let datag;
tg.initData = (data) => {
  const parsedData = JSON.parse(data.data);
  datag = data.data // { field1: "content3", field2: 10 }
  // Используйте полученные данные в вашем веб-приложении
};
   let profName = document.createElement('p'); //создаем параграф
   //выдем имя, "фамилию", через тире username и код языка

   let userid = document.createElement('p'); //создаем еще параграф
   userid.innerText = `${datag}`; //показываем user_id
   usercard.appendChild(userid); //добавляем


   //работает только в attachment menu
   // let pic = document.createElement('img'); //создаем img
   // pic.src = tg.initDataUnsafe.user.photo_url; //задаём src
   // usercard.appendChild(pic); //добавляем элемент в карточку
</script>
</html>
