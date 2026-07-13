<script setup lang="ts">
import { ref, computed } from 'vue'

// Importação dos certificados com o sufixo ?url para o Vite
import certificadoTecnico from '../assets/Certificado_Desenvolvedor_web.pdf?url';
import certificadoStackX from '../assets/Certificado_stackx.png?url';

// IMPORTAÇÃO CORRIGIDA: Apontando exatamente para o arquivo print_muunfree.jpg encontrado na sua pasta assets
import printMuunFree from '../assets/print_muunfree.jpg'; 

defineEmits(['voltar'])

// 1. Botões de filtro superiores
const filtros = ref([
  { id: 'todos', nome: 'Todos', icone: '📂', usarSvg: false },
  { id: 'web_base', nome: 'Web Base', icone: '🌐', usarSvg: false },
  { id: 'controle_versao', nome: 'Controle de Versão', icone: '', usarSvg: true }, 
  { id: 'frameworks', nome: 'Frameworks', icone: '🟢', usarSvg: false },
  { id: 'banco_dados', nome: 'Banco de Dados', icone: '🗄️', usarSvg: false },
  { id: 'back_end', nome: 'Back-End', icone: '⚙️', usarSvg: false }
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
  link: string;
  link_painel_administrativo?: string; 
  repositorio?: string;
  repositorio_painel?: string;      
  repositorio_aplicativo?: string;  
  certificado?: string;
  imagem: string;
}

// 2. Seus Sistemas com Links e Dependências Configurados
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
    link: '#',
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
    link: 'https://makeyour-d-og-oficial-neon.vercel.app/',
    repositorio: 'https://github.com/lucaslopes9/MakeyourDOgOficial.git',
    imagem: 'https://images.unsplash.com/photo-1619740455993-9e612b1af08a?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 6,
    titulo: 'Loja Virtual de Jogos',
    descricao: '🏆 [PROJETO DE CONCLUSÃO DE CURSO LIVRE: desenvolvimento web] Um e-commerce interativo com catálogo responsivo, carrinho de compras funcional e filtros de busca avançados.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: [],
    banco_dados: [],
    controle_versao: ['Git', 'GitHub'],
    back_end: [],
    link: 'https://loja-virtual-de-jogos-finalizada.vercel.app',
    certificado: certificadoTecnico,
    repositorio: '#',
    imagem: 'https://images.unsplash.com/photo-1538481199705-c710c4e965fc?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 7,
    titulo: 'Codifica Projeto Chat',
    descricao: 'Projeto de chat desenvolvido durante o curso livre de desenvolvimento web que simula a comunicação em tempo real entre dois usuários. A aplicação utiliza manipulação dinâmica do DOM e lógica de programação para renderização de mensagens e controle de fluxos da interface.',
    web_base: ['HTML', 'CSS', 'Jquery'],
    frameworks: [], 
    banco_dados: [], 
    controle_versao: ['Git', 'GitHub'],
    back_end: [], 
    certificado: certificadoTecnico,
    repositorio: 'https://github.com/lucaslopes9/codifica-projeto-chat.git',
    link: 'https://codifica-projeto-chat.vercel.app/',
    imagem: 'https://images.unsplash.com/photo-1611532736597-de2d4265fba3?w=500&auto=format&fit=crop&q=60'
  },
  {
    id: 8,
    titulo: 'Muun Free',
    descricao: 'Plataforma desenvolvida em WordPress para conectar programadores freelancers a potenciais clientes. Criado como conclusão de curso na StackX, o projeto utilizou Metodologias Ágeis e a plataforma Bitrix24 para a gestão de tarefas e controle de entregas da equipe.',
    web_base: ['HTML', 'CSS', 'JavaScript'],
    frameworks: ['WordPress'],
    banco_dados: ['MySQL'],
    controle_versao: ['Git', 'GitHub'],
    back_end: ['PHP'],
    link: printMuunFree, // Direciona corretamente para o print real do sistema em tela cheia
    repositorio: '#',
    certificado: certificadoStackX, 
    imagem: 'https://images.unsplash.com/photo-1522071820081-009f0129c71c?w=500&auto=format&fit=crop&q=60'
  }
])

// Filtro computado limpo e tipado para as chaves do objeto Projeto
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