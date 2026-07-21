<script setup lang="ts">
import { ref, computed } from 'vue'

import certificadoTecnico from '../assets/Certificado_Desenvolvedor_web.pdf?url';
import certificadoStackX from '../assets/Certificado_Stackx.png?url';
import printMuunFree from "../assets/print_muunfree.jpg?url";

defineEmits(['voltar'])

// 1. Botões de filtro superiores (Adicionado CI/CD)
const filtros = ref([
  { id: 'todos', nome: 'Todos', icone: '📂', usarSvg: false },
  { id: 'web_base', nome: 'Web Base', icone: '🌐', usarSvg: false },
  { id: 'controle_versao', nome: 'Controle de Versão', icone: '🌿', usarSvg: false }, 
  { id: 'frameworks', nome: 'Frameworks', icone: '🟢', usarSvg: false },
  { id: 'banco_dados', nome: 'Banco de Dados', icone: '🗄️', usarSvg: false },
  { id: 'back_end', nome: 'Back-End', icone: '⚙️', usarSvg: false },
  { id: 'ci_cd', nome: 'CI/CD', icone: '🚀', usarSvg: false }
])

const filtroSelecionado = ref('todos')

interface Projeto {
  id: number;
  titulo: string;
  descricao: string;
  web_base: string[];
  frameworks: string[];
  banco_dados: string[];
  controle_versao: string[];
  back_end: string[];
  ci_cd: string[]; // <-- Adicionado na Interface
  link: string;
  link_painel_administrativo?: string; 
  repositorio?: string;
  repositorio_painel?: string;      
  repositorio_aplicativo?: string;  
  certificado?: string;
  imagem: string;
}

// 2. Seus Sistemas (Com dados de Controle de Versão e CI/CD preenchidos)
const meusProjetos = ref<Projeto[]>([
  {
    id: 1,
    titulo: 'UaiGo - App de Mobilidade',
    descricao: 'Aplicativo de corrida compartilhado com rastreamento e mapas em tempo real para motoristas e passageiros.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['React Native'],
    banco_dados: ['Firebase'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['Node.js'],
    ci_cd: ['GitHub Actions', 'Fastlane'],
    link: 'https://meu-painel-m7i3.vercel.app/', 
    link_painel_administrativo: 'https://meu-painel-m7i3.vercel.app/', 
    repositorio_painel: 'https://github.com/lucaslopes9/meu_Painel.git', 
    repositorio_aplicativo: 'https://github.com/lucaslopes9/Uai_go_aplicativo.git', 
    imagem: 'https://images.unsplash.com/photo-1549576490-b0b4831ef60a?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 2,
    titulo: 'Relógio Digital Dinâmico',
    descricao: 'Aplicação web interativa que realiza consumo de API externa para sincronização da hora real em tempo real, utilizando manipulação de estado do DOM para alternância de temas visuais (Dark/Light Mode).',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [],
    banco_dados: [],
    controle_versao: ['Git', 'GitHub'],
    back_end: [],
    ci_cd: ['Vercel Deploy'],
    link: 'https://relogio-digital-zeta.vercel.app/',
    repositorio: 'https://github.com/lucaslopes9/relogioDigital',
    imagem: 'https://images.unsplash.com/photo-1508962914676-134849a727f0?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 3,
    titulo: 'Conecta Talentos',
    descricao: 'Plataforma corporativa web de recrutamento, triagem e vagas de emprego automatizadas para o mercado de trabalho.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js'],
    banco_dados: ['PostgreSQL'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['Node.js'],
    ci_cd: ['Vercel Deploy'],
    link: 'https://conecta-talentos-lope.vercel.app',
    repositorio: 'https://github.com/lucaslopes9/Conecta_talentos.git',
    imagem: 'https://images.unsplash.com/photo-1586281380349-632531db7ed4?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 4,
    titulo: 'Sistema de Rifas Automatizado',
    descricao: 'Plataforma de sorteios online com geração de cotas e integração completa de pagamentos via Multicaixa Express.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js'],
    banco_dados: ['MySQL'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['PHP', 'Laravel'],
    ci_cd: [],
    link: 'https://github.com/lucaslopes9/Sistemas_de_Rifas.git', 
    repositorio: 'https://github.com/lucaslopes9/Sistemas_de_Rifas.git',
    imagem: 'https://images.unsplash.com/photo-1518609878373-06d740f60d8b?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 5,
    titulo: 'Make Your Dog',
    descricao: 'Sistema completo e responsivo, para gerenciamento, personalização e pedidos de montagem de cachorros-quentes gourmet.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['Vue.js', 'Vue Router'],
    banco_dados: ['JSON Server'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['Node.js'],
    ci_cd: ['Vercel Deploy'],
    link: 'https://makeyour-d-og-oficial-neon.vercel.app/',
    repositorio: 'https://github.com/lucaslopes9/MakeyourDOgOficial.git',
    imagem: 'https://images.unsplash.com/photo-1619740455993-9e612b1af08a?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 6,
    titulo: 'Loja Virtual de Jogos',
    descricao: '🏆 Um e-commerce interativo com catálogo responsivo, carrinho de compras funcional e filtros de busca avançados.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [],
    banco_dados: [],
    controle_versao: ['Git', 'GitHub'],
    back_end: [],
    ci_cd: ['Vercel Deploy'],
    link: 'https://loja-virtual-de-jogos-finalizada.vercel.app',
    certificado: certificadoTecnico,
    repositorio: 'https://github.com/lucaslopes9/Loja_Virtual_de_jogos_finalizada.git', 
    imagem: 'https://images.unsplash.com/photo-1538481199705-c710c4e965fc?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 7,
    titulo: 'Codifica Projeto Chat',
    descricao: 'Projeto de chat desenvolvido que simula a comunicação em tempo real entre dois usuários. A aplicação utiliza manipulação dinâmica do DOM e lógica de programação.',
    web_base: ['HTML', 'CSS', 'Jquery'],
    frameworks: [], 
    banco_dados: [], 
    controle_versao: ['Git', 'GitHub'],
    back_end: [], 
    ci_cd: ['Vercel Deploy'],
    certificado: certificadoTecnico,
    repositorio: 'https://github.com/lucaslopes9/codifica-projeto-chat.git',
    link: 'https://codifica-projeto-chat.vercel.app/',
    imagem: 'https://images.unsplash.com/photo-1611532736597-de2d4265fba3?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 8,
    titulo: 'Muun Free',
    descricao: 'Plataforma desenvolvida em WordPress para conectar programadores freelancers a potenciais clientes. Criado com Metodologias Ágeis e platforma Bitrix24.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['WordPress'],
    banco_dados: ['MySQL'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['PHP'],
    ci_cd: [],
    link: printMuunFree, 
    repositorio: '#',
    certificado: certificadoStackX, 
    imagem: 'https://images.unsplash.com/photo-1522071820081-009f0129c71c?w=500&auto=format&fit=crop&q=60'
  }
])

const projetosFiltrados = computed(() => {
  const filtro = filtroSelecionado.value
  if (filtro === 'todos' || !filtro) {
    return meusProjetos.value
  }
  return meusProjetos.value.filter(projeto => {
    if (filtro in projeto) {
      const categoria = projeto[filtro as keyof typeof projeto]
      return Array.isArray(categoria) && categoria.length > 0
    }
    return false
  })
})

function selecionarFiltro(id: string) {
  filtroSelecionado.value = id
}
</script>

<template>
  <div class="portfolio-container">
    <button class="btn-voltar" @click="$emit('voltar')">⬅ Voltar</button>

    <!-- 1. Barra de Filtros -->
    <div class="filtros-bar">
      <button 
        v-for="filtro in filtros" 
        :key="filtro.id" 
        :class="['filtro-btn', { ativo: filtroSelecionado === filtro.id }]"
        @click="selecionarFiltro(filtro.id)"
      >
        <span>{{ filtro.icone }}</span> {{ filtro.nome }}
      </button>
    </div>

    <!-- 2. Grid de Cards de Projetos -->
    <div class="projetos-grid">
      <div v-for="projeto in projetosFiltrados" :key="projeto.id" class="projeto-card">
        <div class="card-imagem" :style="{ backgroundImage: `url(${projeto.imagem})` }"></div>
        <div class="card-conteudo">
          <h3>{{ projeto.titulo }}</h3>
          <p class="descricao">{{ projeto.descricao }}</p>
          
          <div class="tags">
            <!-- Renderização Dinâmica de Categorias (Incluído controle_versao e ci_cd) -->
            <span v-for="tag in projeto.web_base" :key="tag" class="tag web">{{ tag }}</span>
            <span v-for="tag in projeto.frameworks" :key="tag" class="tag framework">{{ tag }}</span>
            <span v-for="tag in projeto.banco_dados" :key="tag" class="tag bd">{{ tag }}</span>
            <span v-for="tag in projeto.back_end" :key="tag" class="tag back">{{ tag }}</span>
            <span v-for="tag in projeto.controle_versao" :key="tag" class="tag git">{{ tag }}</span>
            <span v-for="tag in projeto.ci_cd" :key="tag" class="tag cicd">{{ tag }}</span>
          </div>

          <div class="card-links">
            <a v-if="projeto.link && projeto.link !== '#'" :href="projeto.link" target="_blank" class="btn-link">Acessar Projeto</a>
            
            <template v-if="projeto.repositorio_painel || projeto.repositorio_aplicativo">
              <a v-if="projeto.repositorio_painel" :href="projeto.repositorio_painel" target="_blank" class="btn-repo">Repo Web (Painel)</a>
              <a v-if="projeto.repositorio_aplicativo" :href="projeto.repositorio_aplicativo" target="_blank" class="btn-repo">Repo App</a>
            </template>
            
            <a v-else-if="projeto.repositorio && projeto.repositorio !== '#'" :href="projeto.repositorio" target="_blank" class="btn-repo">Código Fonte</a>
            
            <a v-if="projeto.certificado" :href="projeto.certificado" target="_blank" class="btn-certificado">📜 Certificado</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.portfolio-container {
  padding: 20px;
  font-family: sans-serif;
  max-width: 1200px;
  margin: 0 auto;
}

.btn-voltar {
  background-color: #333;
  color: #fff;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
  border-radius: 4px;
  margin-bottom: 20px;
  transition: transform 0.2s ease, background-color 0.2s ease, box-shadow 0.2s ease;
}

.btn-voltar:hover {
  transform: translateY(-2px);
  background-color: #444;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
}

.btn-voltar:active {
  transform: translateY(0);
}

.filtros-bar {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 30px;
}

.filtro-btn {
  padding: 8px 16px;
  border: 1px solid #444;
  background-color: #1a1a1a;
  color: #ccc;
  border-radius: 20px;
  cursor: pointer;
  transition: transform 0.25s cubic-bezier(0.175, 0.885, 0.32, 1.275), 
              background-color 0.2s ease, 
              border-color 0.2s ease, 
              box-shadow 0.25s ease,
              color 0.2s ease;
}

.filtro-btn:hover {
  transform: translateY(-4px);
  border-color: #555;
  color: #fff;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.5);
}

.filtro-btn.ativo {
  background-color: #4fc08d;
  color: white;
  border-color: #4fc08d;
}

.filtro-btn.ativo:hover {
  background-color: #5dd59e;
  border-color: #5dd59e;
}

.filtro-btn:active {
  transform: translateY(-1px);
}

.projetos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.projeto-card {
  border: 1px solid #333;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  background: #1e1e1e;
  display: flex;
  flex-direction: column;
}

.card-imagem {
  height: 180px;
  background-size: cover;
  background-position: center;
}

.card-conteudo {
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.card-conteudo h3 {
  margin-top: 0;
  margin-bottom: 10px;
  color: #ffffff;
}

.descricao {
  font-size: 0.9rem;
  color: #bbbbbb;
  flex-grow: 1;
  line-height: 1.4;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin: 15px 0;
}

.tag {
  font-size: 0.75rem;
  padding: 3px 8px;
  border-radius: 4px;
  font-weight: bold;
}

/* Cores das tags em alto contraste no dark mode */
.tag.web { background-color: #1a365d; color: #90cdf4; }
.tag.framework { background-color: #1c4532; color: #9ae6b4; }
.tag.bd { background-color: #744210; color: #fbd38d; }
.tag.back { background-color: #4a128c; color: #e0b0ff; }
.tag.git { background-color: #2c3e50; color: #ecf0f1; } /* Nova cor para Git */
.tag.cicd { background-color: #7f8c8d; color: #f1c40f; } /* Nova cor para CI/CD */

.card-links {
  display: flex;
  gap: 10px;
  margin-top: auto;
  flex-wrap: wrap;
}

.card-links a {
  text-decoration: none;
  font-size: 0.85rem;
  padding: 6px 12px;
  border-radius: 4px;
  text-align: center;
  flex: 1;
  min-width: 100px;
  transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), 
              background-color 0.2s ease, 
              box-shadow 0.2s ease;
}

.card-links a:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
}

.card-links a:active {
  transform: scale(0.98);
}

.btn-link {
  background-color: #4fc08d;
  color: white;
}

.btn-link:hover {
  background-color: #5dd59e;
}

.btn-repo {
  background-color: #333;
  color: white;
  border: 1px solid #444;
}

.btn-repo:hover {
  background-color: #444;
  border-color: #555;
}

.btn-certificado {
  background-color: #ff9800;
  color: white;
}

.btn-certificado:hover {
  background-color: #ffa726;
}

:global(body) {
  background-color: #f8f8f8 !important;
  margin: 0;
  padding: 0;
}


.projeto-card:hover {
  border-color: #3b82f6; /* Azul vibrante */
  box-shadow: 0 6px 15px rgba(59, 130, 246, 0.25); /* Sutil reflexo azulado */
  transform: translateY(-3px); /* Pequeno efeito de elevação */
}



.portfolio-container {
  background-color: #f8f8f8c0;
}
</style>