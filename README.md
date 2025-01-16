<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            text-align: center;
            max-width: 600px;
            padding: 20px;
            border-radius: 10px;
            background: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #2c3e50;
            font-size: 2em;
        }

        p {
            color: #34495e;
            font-size: 1.2em;
            margin-bottom: 20px;
        }

        .message {
            margin: 10px 0;
            padding: 15px;
            border-radius: 5px;
            background-color: #ecf0f1;
            display: block; /* Ensure the message is visible by default */
            transition: all 0.3s ease;
        }

        .message.open {
            background-color: #dff9fb;
            animation: fadeIn 0.5s ease-in-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        input[type="password"] {
            padding: 10px;
            margin-top: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #2ecc71;
            color: #fff;
            cursor: pointer;
            margin-top: 10px;
        }

        button:hover {
            background-color: #27ae60;
        }

        .error {
            color: red;
            display: none;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Pesan Hari Ini 😇</h1>
        <p>Buka satu pesan setiap hari hingga 17 Maret 2025!</p>
        <div id="messages-container"></div>
    </div>
    <script>
        const password = "aneh"; // Password untuk membuka pesan
        const startDate = new Date('2025-01-15'); // Tanggal mulai

        const messageContents = [
            'Jangan Lupa Berdoa Sebelum Tidur 🤍 ☘️',
            'Hari ini adalah hari baru untuk memulai!',
            'Shalom, Kak Nia! ✨ Semoga hari ini penuh sukacita dan berkat yang melimpah! 🌟 Kasih setia TUHAN tak berkesudahan, rahmat-Nya tidak habis-habisnya, selalu baru tiap pagi; besar kesetiaan-Mu!(Ratapan 3:22-23) Hari ini adalah anugerah baru dari Tuhan. Jalani dengan semangat, karena kasih dan penyertaan Tuhan selalu menyertaimu! Tuhan memberkati!🌼',
            'Semoga hari ini penuh dengan damai dan sukacita dari Tuhan!🌟 Tuhan itu dekat dengan orang yang patah hati, dan menyelamatkan orang yang remuk jiwanya. (Mazmur 34:18) Ketika hati merasa lelah, ingatlah bahwa Tuhan selalu dekat dan siap memberikan kekuatan. Terus semangat, Kak! Tuhan memberkati!🌿',
            'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai dan sukacita dari Tuhan! 🌟 "Tuhan itu dekat dengan orang yang patah hati, dan menyelamatkan orang yang remuk jiwanya." (Mazmur 34:18) 🤍 Ketika hati merasa lelah, ingatlah bahwa Tuhan selalu dekat dan siap memberikan kekuatan. Terus semangat, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi semangat baru dan kedamaian dalam hatimu! 🌼 "Bersukacitalah dalam harapan, sabarlah dalam penderitaan, dan bertekunlah dalam doa." (Roma 12:12) 🤍 Terus semangat dan bersandar pada Tuhan, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan pengharapan dan kasih Tuhan! 🌷 "Tuhan adalah tempat perlindungan bagi orang yang tertindas, tempat perlindungan pada waktu kesesakan." (Mazmur 9:9) 🤍 Tuhan adalah tempat perlindungan kita, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga setiap langkahmu penuh dengan berkat Tuhan! 🌸 "Karena itu, saudara-saudaraku yang kekasih, berdirilah teguh, jangan goyah, dan giatlah selalu dalam pekerjaan Tuhan." (1 Korintus 15:58) 🤍 Terus bersemangat dalam melayani! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan sukacita dari Tuhan! 🌿 "Kasih setia TUHAN tak berkesudahan, rahmat-Nya tidak habis-habisnya, selalu baru tiap pagi; besar kesetiaan-Mu!" (Ratapan 3:22-23) 🤍 Jangan pernah menyerah, Tuhan setia menyertai kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi semangat dan kebijaksanaan dalam setiap keputusan yang kamu ambil! 🌼 "Akal budi yang baik memberikan kehidupan, tetapi kebodohan membawa kepada kematian." (Amsal 16:22) 🤍 Berbuatlah bijaksana dalam setiap tindakan, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan semangat dan harapan dari Tuhan! 🌸 "Aku akan memberi kekuatan kepada orang yang lelah, dan menambah semangat kepada orang yang tiada berdaya." (Yesaya 40:29) 🤍 Tuhan memberi kita kekuatan untuk terus melangkah! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi kedamaian dalam hatimu dan berkat dalam setiap langkahmu! 🌿 "Sebab TUHAN memberi kelegaan kepada orang yang letih lesu, dan memuaskan orang yang lapar." (Matius 11:28) 🤍 Tuhan akan memberi kita istirahat dan kelegaan! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberikan kekuatan dalam setiap langkahmu! 🌷 "Orang yang sabar besar pengertiannya." (Amsal 14:29) 🤍 Sabar dan percayakan segala hal pada Tuhan, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai sejahtera dari Tuhan! 🌸 "Aku akan menuntun mereka dalam jalan yang benar." (Mazmur 23:3) 🤍 Tuhan akan memimpin setiap langkah kita menuju jalan yang benar! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberi terang dalam hidupmu! 🌟 "Terang itu bercahaya dalam kegelapan, dan kegelapan itu tidak menguasainya." (Yohanes 1:5) 🤍 Teruslah menjadi terang bagi dunia, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai dan semangat baru dari Tuhan! 🌼 "Karena Tuhan akan menuntun engkau sepanjang hidupmu." (Mazmur 48:14) 🤍 Tuhan selalu menuntun kita dalam setiap langkah hidup. Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan kasih dan semangat Tuhan! 🌸 "Pakai seluruh perlengkapan senjata Allah, supaya kamu dapat bertahan melawan tipu muslihat Iblis." (Efesus 6:11) 🤍 Tuhan memberikan kita kekuatan dan perlindungan untuk bertahan. Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan terus memberikan terang dalam hidupmu! 🌟 "Aku akan memberi mereka hatinya untuk mengenal Aku." (Yeremia 24:7) 🤍 Tuhan selalu memberikan terang bagi mereka yang mencari-Nya. Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai dan semangat baru dari Tuhan! 🌼 "Sebab Allah tidak memberi kita roh ketakutan, melainkan roh kekuatan, kasih, dan ketertiban." (2 Timotius 1:7) 🤍 Terus berani menjalani hidup, karena Tuhan memberi kita kekuatan! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan hati yang penuh kasih! 🌸 "Tuhan itu sabar, panjang sabar dan besar kasih setia-Nya." (Mazmur 103:8) 🤍 Marilah kita melayani dengan penuh kasih! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga kamu penuh dengan semangat dan kepercayaan diri hari ini! 🌸 "Sebab kita adalah karya Tuhan, diciptakan dalam Kristus Yesus untuk melakukan pekerjaan baik." (Efesus 2:10) 🤍 Terus lakukan pekerjaan baik, Kak! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi kekuatan untuk menjalani setiap tantangan dengan iman yang kokoh! 🌿 "Jika Tuhan berkenan, kami akan hidup dan melakukan ini atau itu." (Yakobus 4:15) 🤍 Percayakan hidupmu pada Tuhan! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi damai sejahtera dalam hidupmu! 🌟 "Tetapi kasih karunia Tuhan kami menjadi lebih besar lagi." (Yakobus 4:6) 🤍 Semoga kasih karunia Tuhan selalu melimpah dalam hidupmu! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan kekuatan dan kebijaksanaan dalam menjalani hidup! 🌸 "Tuhan memberikan hikmat; dari mulut-Nya datang pengetahuan dan pengertian." (Amsal 2:6) 🤍 Tuhan akan memberi kita hikmat! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga setiap hari penuh dengan semangat dan kasih Tuhan! 🌿 "Hendaklah kamu bersemangat dan jangan menjadi lemah!" (Ibrani 12:3) 🤍 Jangan pernah menyerah! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan kekuatan baru untuk hari ini! 🌸 "Aku akan memberimu hati yang baru, dan roh yang baru." (Yehezkiel 36:26) 🤍 Tuhan memberi kita kekuatan baru setiap hari! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberi penyertaan dan kedamaian dalam setiap langkah hidupmu! 🌿 "Berserulah kepada-Ku, maka Aku akan menjawab engkau." (Yeremia 33:3) 🤍 Tuhan mendengar setiap doa kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga setiap langkahmu dipenuhi dengan berkat dan kasih Tuhan! 🌷 "Jangan kuatir tentang apapun juga, tetapi nyatakanlah dalam doa, permohonan, dan ucapan syukur kepada Tuhan." (Filipi 4:6) 🤍 Tuhan peduli dengan setiap doa kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan senantiasa memberi kedamaian dalam hatimu! 🌼 "Tuhan adalah terangku dan keselamatanku, kepada siapa aku harus takut?" (Mazmur 27:1) 🤍 Tuhan adalah pelindung kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga setiap harimu penuh dengan berkat Tuhan! 🌷 "Percayalah kepada Tuhan dengan segenap hatimu, dan jangan bersandar kepada pengertianmu sendiri." (Amsal 3:5) 🤍 Tuhan tahu yang terbaik untuk kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberimu kedamaian dan kepercayaan dalam setiap langkah hidupmu! 🌟 "Tuhan itu baik kepada semua orang, dan penuh kasih setia terhadap segala yang dijadikan-Nya." (Mazmur 145:9) 🤍 Tuhan penuh dengan kasih! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga setiap hari penuh dengan semangat dan kebahagiaan! 🌸 "Aku dapat melakukan segala perkara dalam Dia yang memberi kekuatan kepadaku." (Filipi 4:13) 🤍 Dengan Tuhan, kita bisa menghadapi apapun! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi penghiburan dan kekuatan dalam hidupmu! 🌿 "TUHAN itu adalah kekuatanku dan perisaiku; kepada-Nya hatiku percaya, dan aku tertolong." (Mazmur 28:7) 🤍 Tuhan adalah kekuatan kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga setiap langkah hidupmu dipenuhi dengan kasih dan penyertaan Tuhan! 🌷 "Sebab aku tahu bahwa Engkau akan mendengarkan doa kami." (Yohanes 11:42) 🤍 Tuhan mendengarkan doa kita! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberimu hati yang penuh dengan kasih! 🌸 "Tuhan itu baik, menjadi tempat perlindungan pada waktu kesesakan." (Nahum 1:7) 🤍 Tuhan melindungi kita dalam setiap kesesakan! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi damai sejahtera dalam hatimu! 🌿 "Tuhan itu adil, ia akan membalas orang yang jahat." (Mazmur 37:28) 🤍 Tuhan adalah hakim yang adil! Tuhan Yesus memberkati!☘️',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi semangat baru dan kedamaian dalam hatimu! 🌼 Bersukacitalah dalam harapan, sabarlah dalam penderitaan, dan bertekunlah dalam doa. (Roma 12:12) 🤍 Terus semangat dan bersandar pada Tuhan, Kak! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan pengharapan dan kasih Tuhan! 🌷 "Tuhan adalah tempat perlindungan bagi orang yang tertindas, tempat perlindungan pada waktu kesesakan." (Mazmur 9:9) 🤍 Tuhan adalah tempat perlindungan kita, Kak! Tuhan Yesus memberkati! 🤍🌼',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi semangat dan kebijaksanaan dalam setiap keputusan yang kamu ambil! 🌼 "Akal budi yang baik memberikan kehidupan, tetapi kebodohan membawa kepada kematian." (Amsal 16:22) 🤍 Berbuatlah bijaksana dalam setiap tindakan, Kak! Tuhan Yesus memberkati! 🤍🌷',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan semangat dan harapan dari Tuhan! 🌸 "Aku akan memberi kekuatan kepada orang yang lelah, dan menambah semangat kepada orang yang tiada berdaya." (Yesaya 40:29) 🤍 Tuhan memberi kita kekuatan untuk terus melangkah! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberikan kekuatan dalam setiap langkahmu! 🌷 "Orang yang sabar besar pengertiannya." (Amsal 14:29) 🤍 Sabar dan percayakan segala hal pada Tuhan, Kak! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberi terang dalam hidupmu! 🌟 "Terang itu bercahaya dalam kegelapan, dan kegelapan itu tidak menguasainya." (Yohanes 1:5) 🤍 Teruslah menjadi terang bagi dunia, Kak! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai dan semangat baru dari Tuhan! 🌼 "Karena Tuhan akan menuntun engkau sepanjang hidupmu." (Mazmur 48:14) 🤍 Tuhan selalu menuntun kita dalam setiap langkah hidup. Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga Tuhan terus memberikan terang dalam hidupmu! 🌟 "Aku akan memberi mereka hatinya untuk mengenal Aku." (Yeremia 24:7) 🤍 Tuhan selalu memberikan terang bagi mereka yang mencari-Nya. Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga hari ini penuh dengan damai dan semangat baru dari Tuhan! 🌼 "Sebab Allah tidak memberi kita roh ketakutan, melainkan roh kekuatan, kasih, dan ketertiban." (2 Timotius 1:7) 🤍 Terus berani menjalani hidup, karena Tuhan memberi kita kekuatan! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberimu hati yang penuh kasih! 🌸 "Kasih itu sabar, kasih itu murah hati, ia tidak cemburu, ia tidak memegahkan diri dan tidak sombong." (1 Korintus 13:4) 🤍 Mari kita terus melayani dengan hati yang penuh kasih! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga kamu penuh dengan semangat dan kepercayaan diri hari ini! 🌸 "Sebab kita adalah karya Tuhan, diciptakan dalam Kristus Yesus untuk melakukan pekerjaan baik." (Efesus 2:10) 🤍 Terus lakukan pekerjaan baik, Kak! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi kekuatan untuk menjalani setiap tantangan dengan iman yang kokoh! 🌿 "Jika Tuhan berkenan, kami akan hidup dan melakukan ini atau itu." (Yakobus 4:15) 🤍 Percayakan hidupmu pada Tuhan! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberi damai sejahtera dalam hidupmu! 🌟 "Tetapi kasih karunia Tuhan kami menjadi lebih besar lagi." (Yakobus 4:6) 🤍 Semoga kasih karunia Tuhan selalu melimpah dalam hidupmu! Tuhan Yesus memberkati! 🤍🌷',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan kekuatan baru untuk hari ini! 🌸 "Aku akan memberimu hati yang baru, dan roh yang baru." (Yehezkiel 36:26) 🤍 Tuhan memberi kita kekuatan baru setiap hari! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberi penyertaan dan kedamaian dalam setiap langkah hidupmu! 🌿 "Berserulah kepada-Ku, maka Aku akan menjawab engkau." (Yeremia 33:3) 🤍 Tuhan mendengar setiap seruan kita! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga setiap langkahmu dipenuhi dengan berkat dan kasih Tuhan! 🌷 "Jangan kuatir tentang apapun juga, tetapi nyatakanlah dalam doa, permohonan, dan ucapan syukur kepada Tuhan.',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan kekuatan untuk melalui setiap ujian hidup! 🌟 "Tetapi Ia tahu jalan hidupku; seandainya Ia menguji aku, aku akan timbul seperti emas." (Ayub 23:10) 🤍 Dalam setiap ujian, kita akan semakin kuat bersama Tuhan! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu memberi jalan keluar dalam setiap pencobaan! 🌿 "Tidak ada pencobaan yang terjadi di luar kemampuan manusia, sebab Allah setia dan tidak akan membiarkan kamu dicobai melampaui kekuatanmu." (1 Korintus 10:13) 🤍 Percayalah, Tuhan selalu menyediakan jalan keluar! Tuhan Yesus memberkati! 🤍🌷',
    'Shalom, Kak Nia! ✨ Semoga Tuhan selalu membimbingmu dengan kasih-Nya! 🌷 "Tuhan akan memimpin engkau senantiasa, dan Dia akan memberi kekuatan tubuhmu." (Yesaya 58:11) 🤍 Tuhan akan memberikan kekuatan untuk setiap langkah hidupmu! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga setiap harimu penuh dengan semangat yang diberikan oleh Tuhan! 🌿 "Aku ini hendak memberimu masa depan yang penuh harapan. "(Yeremia 29:11) 🤍 Tuhan telah menyiapkan hal yang indah di depanmu, terus maju dengan percaya! Tuhan Yesus memberkati!',
    'Shalom, Kak Nia! ✨ Semoga damai Tuhan selalu mengalir dalam hatimu! 🌸 "Tuhan adalah pelindung hidupku, kepada siapa aku harus takut?" (Mazmur 27:1) 🤍 Jangan takut, Tuhan selalu melindungi setiap langkah kita! Tuhan Yesus memberkati! 🤍🌼',
    'Shalom, Kak Nia! ✨ Semoga Tuhan terus memberi kekuatan dan penghiburan dalam hidupmu! 🌿 "TUHAN itu adalah kekuatanku dan perisaiku; kepada-Nya hatiku percaya, dan aku tertolong." (Mazmur 28:7) 🤍 Dengan Tuhan, kita tidak akan pernah goyah! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga kasih Tuhan selalu hadir di setiap langkahmu! 🌷 "Tuhan itu baik kepada semua orang, dan penuh kasih setia terhadap segala yang dijadikan-Nya." (Mazmur 145:9) 🤍 Kasih Tuhan tak pernah berhenti mengalir untuk kita! Tuhan Yesus memberkati! 🤍💐',
    'Shalom, Kak Nia! ✨ Semoga semangat hidupmu selalu berkobar dengan kekuatan dari Tuhan! 🌸 "Segala perkara dapat kutanggung di dalam Dia yang memberi kekuatan kepadaku." (Filipi 4:13) 🤍 Dengan Tuhan, kita bisa mengatasi segala tantangan hidup! Tuhan Yesus memberkati! 🤍🌷',
    'Shalom, Kak Nia! ✨ Semoga Tuhan memberikan damai dalam setiap aspek hidupmu! 🌿 "Janganlah kuatir akan apapun juga, tetapi nyatakanlah dalam doa permohonan dan ucapan syukur kepada Tuhan." (Filipi 4:6) 🤍 Tuhan mendengarkan doa kita dan memberikan yang terbaik! Tuhan Yesus memberkati! 🤍🌸',
    'Shalom, Kak Nia! ✨ Semoga hari ulang tahunmu penuh dengan berkat dan sukacita dari Tuhan! 🎉 "Sebab Aku ini mengetahui rancangan-rancangan apa yang ada padaku mengenai kamu, yaitu rancangan damai sejahtera dan bukan rancangan kecelakaan, untuk memberikan kepadamu hari depan yang penuh harapan." (Yeremia 29:11) 🤍 Selamat ulang tahun, Kak Nia! Semoga Tuhan terus memberkati setiap langkah hidupmu dengan penuh sukacita dan harapan baru! Tuhan Yesus memberkati! 🤍🌼'
]




        const today = new Date(); // Dapatkan tanggal hari ini
        const container = document.getElementById('messages-container');

        // Hitung berapa hari sejak startDate
        const dayDifference = Math.floor((today - startDate) / (1000 * 3600 * 24));

        // Pastikan pesan tidak melebihi jumlah yang tersedia
        const messageToShow = messageContents[dayDifference];

        if (messageToShow) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('message');
            messageDiv.innerHTML = `
                <p><strong>Tanggal:</strong> ${today.toLocaleDateString()}</p>
                <input type="password" placeholder="Masukkan kata sandi untuk membuka pesan" />
                <button>Buka</button>
                <p class="error">Kata sandi salah!</p>
                <div class="message-content" style="display: none;">
                    <p>${messageToShow}</p>
                </div>
            `;

            const button = messageDiv.querySelector('button');
            const input = messageDiv.querySelector('input');
            const error = messageDiv.querySelector('.error');
            const messageContent = messageDiv.querySelector('.message-content');

            // Menangani klik tombol Buka
            button.addEventListener('click', () => {
                if (input.value === password) {
                    messageDiv.classList.add('open'); // Menampilkan pesan
                    error.style.display = 'none';
                    input.style.display = 'none';
                    button.style.display = 'none';
                    messageContent.style.display = 'block'; // Menampilkan konten pesan
                } else {
                    error.style.display = 'block'; // Menampilkan error jika kata sandi salah
                }
            });

            container.appendChild(messageDiv);
        } else {
            // Jika tidak ada pesan yang sesuai (misalnya, sudah mencapai 17 Februari 2025)
            const endMessageDiv = document.createElement('div');
            endMessageDiv.innerHTML = `<p>Tidak ada pesan lagi yang tersedia.</p>`;
            container.appendChild(endMessageDiv);
        }

        // Fungsi untuk memastikan pesan berubah tepat pada tengah malam
function checkTimeAndUpdate() {
    const currentTime = new Date();
    if (currentTime.getHours() === 0 && currentTime.getMinutes() === 0) {
        updateMessage(); // Update pesan pada jam 00:00
    }
}

// Update pesan saat halaman dimuat pertama kali
updateMessage();

// Set interval untuk memeriksa dan memperbarui pesan setiap menit
setInterval(checkTimeAndUpdate, 60000); // 60000ms = 1 menit






    </script>
</body>
</html>
