# Cat-logo-Gourmet

<?php
  
session_start();
  

  
$receitas = [
  

  
    ["id"=>1,"nome"=>"Bolo de Chocolate","tipo"=>"Doce","descricao"=>"Bolo fofinho com cobertura de chocolate","preco"=>"R$ 25,00","imagem"=>"img/bolo.jpg"],
  

  
    ["id"=>2,"nome"=>"Brigadeiro","tipo"=>"Doce","descricao"=>"Doce brasileiro feito com leite condensado e chocolate","preco"=>"R$ 8,00","imagem"=>"img/brigadeiro.jpg"],
  

  
    ["id"=>3,"nome"=>"Pudim","tipo"=>"Doce","descricao"=>"Pudim cremoso com calda de caramelo","preco"=>"R$ 18,00","imagem"=>"img/pudim.jpg"],
  

  
    ["id"=>4,"nome"=>"Torta de Morango","tipo"=>"Doce","descricao"=>"Torta com creme e morangos frescos","preco"=>"R$ 30,00","imagem"=>"img/torta.jpg"],
  

  
    ["id"=>5,"nome"=>"Panqueca Doce","tipo"=>"Doce","descricao"=>"Panqueca recheada com chocolate","preco"=>"R$ 15,00","imagem"=>"img/panqueca.jpg"],
  

  
    ["id"=>6,"nome"=>"Lasanha","tipo"=>"Salgado","descricao"=>"Lasanha de carne com queijo","preco"=>"R$ 35,00","imagem"=>"img/lasanha.jpg"],
  

  
    ["id"=>7,"nome"=>"Pizza","tipo"=>"Salgado","descricao"=>"Pizza tradicional de queijo","preco"=>"R$ 50,00","imagem"=>"img/pizza.jpg"],
  

  
    ["id"=>8,"nome"=>"Hambúrguer","tipo"=>"Salgado","descricao"=>"Hambúrguer artesanal","preco"=>"R$ 28,00","imagem"=>"img/hamburguer.jpg"],
  

  
    ["id"=>9,"nome"=>"Coxinha","tipo"=>"Salgado","descricao"=>"Salgado de frango frito","preco"=>"R$ 10,00","imagem"=>"img/coxinha.jpg"],
  

  
    ["id"=>10,"nome"=>"Arroz com Frango","tipo"=>"Salgado","descricao"=>"Arroz temperado com frango","preco"=>"R$ 22,00","imagem"=>"img/arroz.jpg"],
  
];
  

  
function filtrarReceitas($receitas, $tipo) {
  
    return array_filter($receitas, function($r) use ($tipo) {
  
        return $r['tipo'] == $tipo;
  
    });
  
}
  

  
if (!isset($_SESSION['novas_receitas'])) {
  
    $_SESSION['novas_receitas'] = [];
  
}
  

  
$receitas = array_merge($receitas, $_SESSION['novas_receitas']);
  

  
$tipo = $_GET['tipo'] ?? '';
  
$busca = $_GET['busca'] ?? '';
  

  
$resultado = $receitas;
  

  
if ($tipo) {
  
    $resultado = filtrarReceitas($resultado, $tipo);
  
}
  

  
if ($busca) {
  
    $resultado = array_filter($resultado, function ($r) use ($busca) {
  
        return stripos($r['nome'], $busca) !== false;
  
    });
  
}
  

  
if (isset($_GET['logout'])) {
  
    session_destroy();
  
    header("Location: index.php");
  
    exit;
  
}
  
?><!DOCTYPE html><html lang="pt-br"><head><meta charset="UTF-8">



<title>Catálogo Gourmet</title>



<link rel="stylesheet" href="style.css">

</head><body><nav><a href="#home">Home</a>

<a href="#filtrar">Filtrar</a>

<a href="#login">Login</a>

<a href="#cadastro">Cadastrar</a>



<?php if(isset($_SESSION['logado'])): ?>

    <a href="?logout=true">Logout</a>

<?php endif; ?>

</nav><div class="hero"><h1>Catálogo Gourmet</h1>



<p>As melhores receitas doces e salgadas</p>

</div><section id="home"><h1>Nossas Receitas</h1>



<div class="container-cards">



    <?php foreach($resultado as $r): ?>



        <div class="card">



            <img src="<?= $r['imagem'] ?>">



            <div class="card-content">



                <h2><?= htmlspecialchars($r['nome']) ?></h2>



                <div class="tipo">

                    <?= htmlspecialchars($r['tipo']) ?>

                </div>



                <p><?= htmlspecialchars($r['descricao']) ?></p>



                <h3 class="preco">

                    <?= htmlspecialchars($r['preco']) ?>

                </h3>



                <a class="btn" href="?detalhe=<?= $r['id'] ?>">

                    Ver mais

                </a>



            </div>



        </div>



    <?php endforeach; ?>



</div>

</section><section id="filtrar"><h1>Filtrar Receitas</h1>



<form method="GET">



    <select name="tipo">



        <option value="">Todos</option>



        <option value="Doce"

            <?= $tipo=="Doce" ? "selected" : "" ?>>

            Doce

        </option>



        <option value="Salgado"

            <?= $tipo=="Salgado" ? "selected" : "" ?>>

            Salgado

        </option>



    </select>



    <input type="text"

           name="busca"

           placeholder="Buscar receita">



    <button type="submit">

        Aplicar filtros

    </button>



</form>

</section><?php
  
if(isset($_GET['detalhe'])){
  

  
    foreach($receitas as $r){
  

  
        if($r['id'] == $_GET['detalhe']){
  

  
            echo "
  
            <div class='detalhe'>
  

  
                <h1>{$r['nome']}</h1>
  

  
                <img src='{$r['imagem']}'>
  

  
                <p>{$r['descricao']}</p>
  

  
                <h2 class='preco'>{$r['preco']}</h2>
  

  
                <br>
  

  
                <a class='btn' href='#home'>Voltar</a>
  

  
            </div>
  
            ";
  
        }
  
    }
  
}
  
?><footer><p>Projeto de Catálogo de Receitas em PHP</p>

</footer></body></html>
















*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family: Arial, Helvetica, sans-serif;
    background:#f5f5f5;
    color:#333;
}

/* ========================= */
/* NAVBAR */
/* ========================= */

nav{
    background:#111827;
    padding:20px;
    display:flex;
    justify-content:center;
    gap:30px;
    position:sticky;
    top:0;
}

nav a{
    color:white;
    text-decoration:none;
    font-weight:bold;
    transition:0.3s;
}

nav a:hover{
    color:#f59e0b;
}

/* ========================= */
/* HERO */
/* ========================= */

.hero{
    height:300px;
    background:url('img/banner.jpg') center/cover;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
    color:white;
    text-align:center;
}

.hero h1{
    font-size:50px;
    margin-bottom:10px;
    text-shadow:2px 2px 10px black;
}

.hero p{
    font-size:20px;
    text-shadow:2px 2px 10px black;
}

/* ========================= */
/* SECTIONS */
/* ========================= */

section{
    padding:50px;
}

section h1{
    text-align:center;
    margin-bottom:30px;
    font-size:35px;
}

/* ========================= */
/* CARDS */
/* ========================= */

.container-cards{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(300px,1fr));
    gap:30px;
}

.card{
    background:white;
    border-radius:20px;
    overflow:hidden;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
    transition:0.3s;
}

.card:hover{
    transform:translateY(-10px);
}

.card img{
    width:100%;
    height:220px;
    object-fit:cover;
}

.card-content{
    padding:20px;
    text-align:center;
}

.card h2{
    margin-bottom:10px;
}

.tipo{
    background:#f59e0b;
    color:white;
    padding:5px 15px;
    border-radius:20px;
    display:inline-block;
    margin-bottom:15px;
}

.btn{
    display:inline-block;
    margin-top:15px;
    padding:10px 20px;
    background:#111827;
    color:white;
    border-radius:10px;
    text-decoration:none;
    transition:0.3s;
}

.btn:hover{
    background:#f59e0b;
}

/* ========================= */
/* FORMULÁRIOS */
/* ========================= */

form{
    max-width:500px;
    margin:auto;
    background:white;
    padding:30px;
    border-radius:20px;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
}

input,
select,
textarea,
button{
    width:100%;
    padding:15px;
    margin-bottom:15px;
    border-radius:10px;
    border:1px solid #ccc;
    font-size:16px;
}

button{
    background:#111827;
    color:white;
    border:none;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    background:#f59e0b;
}

/* ========================= */
/* DETALHES */
/* ========================= */

.detalhe{
    max-width:700px;
    margin:40px auto;
    background:white;
    padding:30px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
}

.detalhe img{
    width:100%;
    max-width:500px;
    border-radius:20px;
    margin:20px 0;
}

/* ========================= */
/* FOOTER */
/* ========================= */

footer{
    background:#111827;
    color:white;
    text-align:center;
    padding:20px;
    margin-top:50px;
}
