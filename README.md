import streamlit as st
import random

# Configuración inicial
st.set_page_config(page_title="Potro Internacional 🐎", page_icon="🐎", layout="wide")
st.title("Potro Internacional 🐎")
st.markdown("¡Hola! Soy tu asistente en tratados internacionales. ¿En qué puedo ayudarte? 🌟")

# Estado de la conversación
if 'quiz_active' not in st.session_state:
    st.session_state.quiz_active = False

# Base de conocimiento EXPANDIDA y DETALLADA
knowledge_base = {
    "unidad_1": {
        "titulo": "📚 Contexto teórico e histórico: De la Segunda Guerra Mundial a la Globalización",
        "emoji": "📚",
        "descripcion": "Evolución histórica de los tratados internacionales desde la antigüedad hasta la era contemporánea",
        "temas": {
            "modelos_integracion": {
                "pregunta": "Modelos de integración regional y económica",
                "respuesta": "Los procesos de integración regional representan diferentes niveles de cooperación económica y política entre Estados soberanos, desde acuerdos básicos de comercio hasta uniones políticas completas.",
                "emoji": "🔄",
                "subtemas": {
                    "definicion": "🔄 **Definición**: Proceso multidimensional donde Estados nacionales voluntariamente ceden atributos de soberanía para resolver conflictos conjuntamente y alcanzar objetivos comunes",
                    "niveles": "📊 **Niveles de integración**: \n- Zona de libre comercio (eliminación aranceles)\n- Unión aduanera (arancel externo común)\n- Mercado común (libre movimiento factores)\n- Unión económica (armonización políticas)\n- Unión política (integración completa)",
                    "teorias": "🎓 **Teorías fundamentales**: \n- Funcionalismo (David Mitrany)\n- Neofuncionalismo (Ernst Haas)\n- Intergubernamentalismo (Andrew Moravcsik)",
                    "ejemplos": "🌍 **Ejemplos regionales**: \n- UE (más avanzada)\n- MERCOSUR (América del Sur)\n- ASEAN (Sureste Asiático)\n- CARICOM (Caribe)"
                }
            },
            "guerra_fria": {
                "pregunta": "Antecedentes, desarrollo y consecuencias de la Guerra Fría",
                "respuesta": "Período de tensión geopolítica entre 1947-1991 que dividió al mundo en dos bloques antagónicos liderados por Estados Unidos y la Unión Soviética, moldeando el sistema internacional moderno.",
                "emoji": "❄️",
                "subtemas": {
                    "origen": "🕰️ **Origen**: Conferencias de Yalta y Potsdam (1945), Doctrina Truman (1947), Plan Marshall (1948)",
                    "bloques": "⚔️ **Bloques enfrentados**: \n- OTAN (Occidental capitalista)\n- Pacto de Varsovia (Oriental socialista)\n- Movimiento No Alineado",
                    "crisis": "🚨 **Principales crisis**: \n- Bloqueo de Berlín (1948-49)\n- Guerra de Corea (1950-53)\n- Crisis de los misiles Cuba (1962)\n- Guerra de Vietnam (1955-75)",
                    "consecuencias": "📈 **Impacto en tratados**: \n- Creación sistema Bretton Woods\n- Proliferación acuerdos bilaterales\n- Carrera armamentística nuclear\n- Diplomacia de contención"
                }
            },
            "caida_socialismo": {
                "pregunta": "Caída del bloque socialista y nuevo orden mundial", 
                "respuesta": "Proceso de desintegración del bloque soviético entre 1989-1991 que transformó radicalmente el panorama geopolítico global y permitió la expansión del capitalismo.",
                "emoji": "🧱",
                "subtemas": {
                    "cronologia": "📅 **Cronología clave**: \n- 1985: Perestroika y Glasnost\n- 1989: Caída Muro Berlín\n- 1990: Reunificación Alemania\n- 1991: Disolución URSS",
                    "causas": "🔍 **Causas estructurales**: \n- Estancamiento económico\n- Carrera armamentística\n- Movimientos disidentes\n- Reformas Gorbachov",
                    "consecuencias": "🌐 **Nuevo orden mundial**: \n- Fin bipolaridad\n- Expansión OTAN\n- Surgimiento nuevas potencias\n- Globalización acelerada",
                    "tratados": "📜 **Impacto en tratados**: \n- Nuevos acuerdos comerciales\n- Expansión OMC\n- Integración Europa Oriental"
                }
            },
            "globalizacion": {
                "pregunta": "Neoliberalismo y Globalización económica",
                "respuesta": "Proceso de integración económica mundial caracterizado por la liberalización comercial, flujos financieros transfronterizos y expansión de corporaciones multinacionales.",
                "emoji": "🌐",
                "subtemas": {
                    "definicion": "📖 **Definición**: 'Prolongación más allá de fronteras nacionales de las mismas fuerzas del mercado que durante siglos han operado a niveles de actividad económica humana'",
                    "dimensiones": "📊 **Dimensiones**: \n- Económica (comercio, finanzas)\n- Política (gobernanza global)\n- Cultural (homogeneización)\n- Tecnológica (TICs)",
                    "instituciones": "🏛️ **Instituciones clave**: \n- Fondo Monetario Internacional\n- Banco Mundial\n- Organización Mundial del Comercio\n- G7/G20",
                    "criticas": "⚖️ **Debates y críticas**: \n- Asimetrías Norte-Sur\n- Pérdida soberanía nacional\n- Homogeneización cultural\n- Crisis financieras"
                }
            },
            "regionalismo": {
                "pregunta": "Regionalismo contemporáneo",
                "respuesta": "Fenómeno de creación de acuerdos de integración regional que complementa y a veces compite con el proceso de globalización.",
                "emoji": "🤝",
                "subtemas": {
                    "definicion": "📍 **Definición**: Integración económico-comercial al mundo dentro de un área geográfica común contigua o determinada",
                    "tipos": "🔄 **Nuevo regionalismo**: \n- Abierto vs cerrado\n- Norte-Norte vs Norte-Sur\n- Regionalismo profundo",
                    "motivaciones": "🎯 **Motivaciones**: \n- Eficiencia económica\n- Poder de negociación\n- Seguridad regional\n- Identidad cultural",
                    "ejemplos": "🌎 **Ejemplos actuales**: \n- Unión Europea\n- USMCA/T-MEC\n- Alianza del Pacífico\n- RCEP asiático"
                }
            }
        }
    },
    "unidad_2": {
        "titulo": "🏛️ Organismos Internacionales: Acuerdos que les regulan",
        "emoji": "🏛️",
        "descripcion": "Análisis de los principales organismos internacionales que regulan el comercio global",
        "temas": {
            "oma": {
                "pregunta": "Organización Mundial de Aduanas (OMA)",
                "respuesta": "Organismo intergubernamental independiente que establece estándares internacionales para la administración aduanera y facilita el comercio legítimo.",
                "emoji": "📦",
                "subtemas": {
                    "historia": "📜 **Historia**: Fundada en 1952 como Consejo de Cooperación Aduanera, renombrada OMA en 1994. 183 miembros actuales",
                    "estructura": "🏢 **Estructura**: \n- Consejo (órgano decisorio)\n- Comité Técnico Sistema Armonizado\n- Comité de Facilitación\n- Comité de Aplicación Normas",
                    "instrumentos": "🛠️ **Instrumentos clave**: \n- Sistema Armonizado (6 dígitos)\n- Convenio de Kioto revisado\n- Marco SAFE\n- Programa OEA",
                    "funciones": "🎯 **Funciones principales**: \n- Armonización procedimientos\n- Facilitación comercio\n- Seguridad cadena suministro\n- Capacitación aduanera"
                }
            },
            "omc": {
                "pregunta": "Organización Mundial del Comercio (OMC)",
                "respuesta": "Única organización internacional que se ocupa de las normas que rigen el comercio entre los países, estableciendo el marco jurídico e institucional del sistema multilateral de comercio.",
                "emoji": "📊",
                "subtemas": {
                    "fundacion": "🏛️ **Fundación**: Creada en 1995 por el Acuerdo de Marrakech, sucesora del GATT. 164 miembros representando >98% comercio mundial",
                    "principios": "⚖️ **Principios fundamentales**: \n- No discriminación (NMF)\n- Trato nacional\n- Transparencia\n- Competencia leal",
                    "acuerdos": "📑 **Acuerdos principales**: \n- Acuerdo sobre la OMC\n- GATT 1994 (bienes)\n- GATS (servicios)\n- ADPIC (propiedad intelectual)",
                    "mecanismos": "⚔️ **Mecanismos clave**: \n- Negociaciones comerciales\n- Solución diferencias\n- Exámenes políticas comerciales\n- Asistencia técnica"
                }
            },
            "cic": {
                "pregunta": "Cámara Internacional de Comercio (CCI)", 
                "respuesta": "Organización empresarial que representa los intereses de empresas de todos los sectores en más de 130 países, actuando como voz unificada de la comunidad empresarial mundial.",
                "emoji": "💼",
                "subtemas": {
                    "historia": "📅 **Historia**: Fundada en 1919 en París para reconstruir economía mundial tras Primera Guerra Mundial",
                    "gobernanza": "👥 **Gobernanza**: \n- Presidente: María Fernanda Garza (México)\n- Secretario General: John W.H. Denton AO\n- Consejo Mundial\n- Comisiones nacionales",
                    "herramientas": "🛠️ **Herramientas comerciales**: \n- Incoterms® 2020 (11 términos)\n- Reglas UCP 600 (créditos)\n- Corte Arbitral Internacional\n- Códigos éticos",
                    "iniciativas": "🌟 **Iniciativas actuales**: \n- Economía digital\n- Sostenibilidad empresarial\n- Inclusión financiera\n- Comercio electrónico"
                }
            },
            "itc": {
                "pregunta": "Centro de Comercio Internacional (ITC)", 
                "respuesta": "Agencia conjunta de la OMC y las Naciones Unidas que ayuda a las pequeñas y medianas empresas de países en desarrollo a integrarse en la economía global.",
                "emoji": "📈",
                "subtemas": {
                    "mision": "🎯 **Misión**: 'Fomentar la internacionalización inclusiva en países en desarrollo y economías en transición'",
                    "enfoques": "📊 **Áreas de enfoque**: \n- Competitividad PYMES\n- Sostenibilidad y comercio verde\n- Inclusión y equidad",
                    "programas": "🚀 **Programas emblemáticos**: \n- SheTrades (mujeres)\n- GreenToCompete (sostenibilidad)\n- Alliances for Action (cadenas valor)",
                    "herramientas": "💻 **Herramientas digitales**: \n- Trade Map (estadísticas)\n- Market Access Map (aranceles)\n- SME Trade Academy (capacitación)"
                }
            },
            "acuerdos_omc": {
                "pregunta": "Acuerdos específicos de la OMC",
                "respuesta": "Conjunto de acuerdos multilaterales que regulan aspectos específicos del comercio internacional bajo el paraguas de la OMC.",
                "emoji": "📋",
                "subtemas": {
                    "antidumping": "⚖️ **Acuerdo Antidumping**: Permite imponer derechos adicionales cuando productos son exportados por debajo de su valor normal",
                    "salvaguardias": "🛡️ **Acuerdo sobre Salvaguardias**: Medidas temporales ante aumentos imprevistos de importaciones que causan daño grave",
                    "msf": "🌱 **Acuerdo MSF**: Medidas sanitarias y fitosanitarias para protección vida humana, animal y vegetal",
                    "adpic": "💡 **Acuerdo ADPIC**: Aspectos de derechos de propiedad intelectual relacionados con el comercio",
                    "subvenciones": "💰 **Acuerdo sobre Subvenciones**: Disciplina sobre subvenciones que distorsionan comercio y medidas compensatorias"
                }
            }
        }
    },
    "unidad_3": {
        "titulo": "🌍 Acuerdos y Tratados Internacionales", 
        "emoji": "🌍",
        "descripcion": "Marco jurídico y práctico de los tratados internacionales en el contexto global",
        "temas": {
            "conceptos": {
                "pregunta": "Conceptos básicos de tratados internacionales",
                "respuesta": "Acuerdo internacional celebrado por escrito entre Estados y regido por el derecho internacional, ya conste en un instrumento único o en dos o más instrumentos conexos.",
                "emoji": "📜",
                "subtemas": {
                    "definicion": "📖 **Definición legal**: 'Acuerdo internacional celebrado por escrito entre Estados y regido por el derecho internacional' (Convención de Viena 1969)",
                    "elementos": "🔍 **Elementos esenciales**: \n- Sujetos derecho internacional\n- Consentimiento mutuo\n- Objeto lícito\n- Forma escrita",
                    "clasificacion": "📂 **Clasificación**: \n- Bilaterales vs multilaterales\n- Leyes vs contratos\n- Autoejecutables vs no autoejecutables",
                    "denominaciones": "🏷️ **Denominaciones**: Tratado, convenio, pacto, acuerdo, carta, estatuto, etc."
                }
            },
            "viena": {
                "pregunta": "Convención de Viena sobre el Derecho de los Tratados (1969)",
                "respuesta": "Tratado internacional que codifica las normas de derecho internacional consuetudinario que rigen los tratados entre Estados, estableciendo el marco jurídico para su celebración, aplicación y terminación.",
                "emoji": "🏛️",
                "subtemas": {
                    "alcance": "📏 **Alcance**: Aplica a tratados entre Estados celebrados por escrito y regidos por derecho internacional (Art. 1-2)",
                    "principios": "⚖️ **Principios fundamentales**: \n- Pacta sunt servanda\n- Buena fe\n- Consentimiento libre\n- Irretroactividad",
                    "procedimientos": "🔄 **Procedimientos**: \n- Negociación\n- Adopción texto\n- Autenticación\n- Consentimiento obligarse",
                    "reservas": "📝 **Reservas**: Declaración unilateral que excluye/modifica efectos jurídicos de ciertas disposiciones (Art. 19-23)"
                }
            },
            "historicos": {
                "pregunta": "Evolución histórica de los tratados",
                "respuesta": "Los tratados internacionales han evolucionado desde acuerdos básicos entre civilizaciones antiguas hasta complejos instrumentos jurídicos que regulan todos los aspectos de las relaciones internacionales.",
                "emoji": "🕰️",
                "subtemas": {
                    "antiguos": "🏺 **Tratados antiguos**: \n- Tratado Qadesh (1259 a.C.) - Egipto/Hititas\n- Tratados mesopotámicos (2500 a.C.)\n- Triple Alianza (México prehispánico)",
                    "modernos": "📜 **Era moderna**: \n- Paz Westfalia (1648) - Estado soberano\n- Congreso Viena (1815) - Sistema interestatal\n- Tratado Versalles (1919) - Sociedad Naciones",
                    "contemporaneos": "🌐 **Era contemporánea**: \n- Carta ONU (1945) - Sistema multilateral\n- Acuerdo Marrakech (1994) - OMC\n- Acuerdo París (2015) - Cambio climático",
                    "tendencias": "📈 **Tendencias actuales**: \n- Multilateralismo complejo\n- Tratados megarregionales\n- Soft law internacional\n- Gobernanza sectorial"
                }
            },
            "regionales": {
                "pregunta": "Acuerdos internacionales por región",
                "respuesta": "Panorama de los principales acuerdos comerciales y de integración organizados por regiones geográficas.",
                "emoji": "🗺️",
                "subtemas": {
                    "asia": "🐉 **Asia**: \n- RCEP (Asociación Económica Integral Regional)\n- ASEAN (Asociación Naciones Sureste Asiático)\n- APEC (Foro Cooperación Económica Asia-Pacífico)",
                    "europa": "🇪🇺 **Europa**: \n- Unión Europea (integración profunda)\n- AELC (Asociación Europea Libre Comercio)\n- Acuerdo Cielos Abiertos UE-EEUU",
                    "america": "🌎 **América**: \n- USMCA/T-MEC (América del Norte)\n- MERCOSUR (América del Sur)\n- Alianza del Pacífico\n- CARICOM (Caribe)",
                    "africa": "🦁 **África**: \n- AfCFTA (Área Continental Libre Comercio)\n- SADC (Comunidad Desarrollo África Austral)\n- ECOWAS (Comunidad Económica Estados África Occidental)"
                }
            }
        }
    },
    "unidad_4": {
        "titulo": "🇲🇽 Principales Acuerdos Internacionales de México", 
        "emoji": "🇲🇽", 
        "descripcion": "Análisis de la política comercial mexicana y sus principales acuerdos internacionales",
        "temas": {
            "caracteristicas": {
                "pregunta": "Características generales y normatividad aplicable",
                "respuesta": "México cuenta con una de las redes más extensas de tratados comerciales en el mundo, posicionándose como puente comercial estratégico entre América, Europa y Asia.",
                "emoji": "🌉",
                "subtemas": {
                    "posicion": "📍 **Posición estratégica**: \n- 12 Tratados de Libre Comercio\n- 32 Acuerdos de Promoción y Protección Recíproca de Inversiones\n- Miembro OCDE, OMC, Alianza del Pacífico",
                    "marco_legal": "⚖️ **Marco legal interno**: \n- Constitución Política (Art. 76, 89, 133)\n- Ley sobre Celebración de Tratados\n- Ley de Comercio Exterior\n- Reglamentos aduaneros",
                    "ventajas": "🚀 **Ventajas competitivas**: \n- Acceso preferencial a +1,500 millones de consumidores\n- Diversificación mercados de exportación\n- Atracción de inversión extranjera directa",
                    "instituciones": "🏢 **Instituciones clave**: \n- Secretaría de Relaciones Exteriores\n- Secretaría de Economía\n- Servicio de Administración Tributaria\n- Bancomext"
                }
            },
            "proceso": {
                "pregunta": "Proceso de aprobación de acuerdos internacionales",
                "respuesta": "Procedimiento constitucionalmente establecido para la celebración, aprobación y entrada en vigor de tratados internacionales en México.",
                "emoji": "📑",
                "subtemas": {
                    "etapas": "🔄 **Etapas del proceso**: \n1. Negociación (Ejecutivo Federal)\n2. Firma (Presidente/Secretario)\n3. Aprobación Senado (Art. 76)\n4. Ratificación\n5. Publicación DOF\n6. Entrada en vigor",
                    "competencias": "👥 **Competencias constitucionales**: \n- Presidente: Negociación y firma\n- Senado: Aprobación (2/3 partes)\n- Suprema Corte: Controversias constitucionales",
                    "plazos": "⏰ **Plazos y procedimientos**: \n- Negociación: 1-3 años promedio\n- Aprobación senatorial: 30-60 días\n- Ratificación: Depende de contrapartes\n- Entrada vigor: 30-90 días tras ratificación",
                    "control": "🔍 **Control constitucional**: \n- Juicio de amparo indirecto\n- Controversias constitucionales\n- Acciones de inconstitucionalidad"
                }
            },
            "tlcs": {
                "pregunta": "Tratados de Libre Comercio de México",
                "respuesta": "Red de acuerdos comerciales que eliminan o reducen sustancialmente las barreras arancelarias y no arancelarias al comercio de bienes y servicios.",
                "emoji": "🤝",
                "subtemas": {
                    "tmec": "🇺🇸 **T-MEC (2020)**: \n- Estados Unidos, Canadá\n- 75% contenido regional automotriz\n- Capítulo laboral y ambiental\n- Resolución controversias modernizada",
                    "tlcue": "🇪🇺 **TLCUE (2000)**: \n- Unión Europea (27 países)\n- Eliminación 99% aranceles\n- Comercio servicios e inversiones\n- Diálogo político reforzado",
                    "otros": "🌍 **Otros TLCs importantes**: \n- ACE con Japón\n- TLC con Israel\n- Alianza del Pacífico\n- Acuerdo con Reino Unido post-Brexit",
                    "beneficios": "📈 **Impacto económico**: \n- México: 2° socio comercial EEUU\n- 80% exportaciones a TLCs\n- Diversificación exportadora\n- Encadenamientos productivos"
                }
            },
            "appris": {
                "pregunta": "Acuerdos para la Promoción y Protección Recíproca de Inversiones",
                "respuesta": "Tratados bilaterales que establecen marcos jurídicos estables y predecibles para la inversión extranjera directa entre los países signatarios.",
                "emoji": "💰",
                "subtemas": {
                    "objetivos": "🎯 **Objetivos principales**: \n- Protección inversiones\n- No discriminación\n- Trato justo y equitativo\n- Libre transferencia utilidades",
                    "clausulas": "📝 **Cláusulas esenciales**: \n- Trato nación más favorecida\n- Trato nacional\n- Expropiación e indemnización\n- Solución controversias inversionista-Estado",
                    "evolucion": "🔄 **Evolución reciente**: \n- Mayor equilibrio derechos/obligaciones\n- Excepciones regulatorias\n- Transparencia procedimientos\n- Desarrollo sostenible",
                    "impacto": "📊 **Impacto en México**: \n- 3er destino IED América Latina\n- Diversificación sectores\n- Transferencia tecnología\n- Generación empleo"
                }
            }
        }
    },
    "unidad_5": {
        "titulo": "📊 Efectos de los Tratados Internacionales en la Economía Mexicana",
        "emoji": "📊",
        "descripcion": "Análisis del impacto económico y distributivo de los acuerdos comerciales en México",
        "temas": {
            "balanza_pagos": {
                "pregunta": "Balanza de Pagos y su estructura",
                "respuesta": "Registro sistemático de todas las transacciones económicas entre residentes de México y residentes del resto del mundo durante un período determinado.",
                "emoji": "📈",
                "subtemas": {
                    "componentes": "💳 **Componentes principales**: \n- Cuenta corriente (bienes, servicios, renta, transferencias)\n- Cuenta capital (transferencias capital, activos no financieros)\n- Cuenta financiera (inversión, derivados, reservas)",
                    "tendencias": "📊 **Tendencias México**: \n- Déficit crónico cuenta corriente (2-3% PIB)\n- Superávit cuenta financiera por IED\n- Reservas internacionales estables\n- Deuda externa moderada",
                    "indicadores": "🔍 **Indicadores clave**: \n- Cobertura importaciones por reservas\n- Servicio deuda externa/exportaciones\n- Posición inversión internacional\n- Tipo de cambio real",
                    "politicas": "🎯 **Políticas relacionadas**: \n- Tipo cambio flexible\n- Reglas flujos capital\n- Acuerdos swap divisas\n- Diversificación mercados"
                }
            },
            "balanza_comercial": {
                "pregunta": "Balanza Comercial y comercio exterior",
                "respuesta": "Componente de la balanza de pagos que registra el valor de las exportaciones e importaciones de bienes, reflejando la competitividad internacional de la economía.",
                "emoji": "⚖️",
                "subtemas": {
                    "estructura": "🏭 **Estructura comercial**: \n- Exportaciones: 80% manufacturas, 10% petroleras, 10% agropecuarias\n- Importaciones: bienes intermedios (65%), consumo (15%), capital (20%)",
                    "socios": "🤝 **Principales socios**: \n- EEUU (80% exportaciones, 45% importaciones)\n- China (2% exportaciones, 20% importaciones)\n- Unión Europea (5% exportaciones, 12% importaciones)",
                    "saldos": "📊 **Saldos regionales**: \n- Superávit con América del Norte\n- Déficit con Asia (especialmente China)\n- Equilibrio con Europa y América Latina",
                    "competitividad": "🚀 **Indicadores competitividad**: \n- Participación mercados internacionales\n- Diversificación productos y destinos\n- Contenido nacional exportaciones\n- Encadenamientos productivos"
                }
            },
            "distribucion": {
                "pregunta": "Efecto de distribución en la economía nacional",
                "respuesta": "Impacto diferenciado de la liberalización comercial across sectores económicos, regiones geográficas y grupos sociales en México.",
                "emoji": "🏭",
                "subtemas": {
                    "sectores": "🏗️ **Impacto sectorial**: \n- Ganadores: automotriz, electrónica, aeroespacial\n- Perdedores: textiles, calzado, juguetes\n- Mixto: agrícola (ganan frutas/verduras, pierden granos)",
                    "regional": "🗺️ **Distribución regional**: \n- Norte: mayor integración cadenas globales\n- Centro: manufactura avanzada\n- Sur: menor integración, agricultura tradicional",
                    "social": "👥 **Impacto social**: \n- Creación empleo sector exportador\n- Pérdida empleo manufacturas tradicionales\n- Migración interna hacia zonas exportadoras\n- Diferenciación salarial por habilidades",
                    "politicas": "🛡️ **Políticas compensatorias**: \n- Programas de reconversión productiva\n- Apoyo a pequeñas y medianas empresas\n- Desarrollo clusters regionales\n- Educación y capacitación técnica"
                }
            },
            "otros_efectos": {
                "pregunta": "Otros efectos económicos y estructurales",
                "respuesta": "Impactos adicionales de los tratados comerciales en la estructura productiva, innovación tecnológica y desarrollo institucional de México.",
                "emoji": "🔍",
                "subtemas": {
                    "productividad": "📈 **Productividad y eficiencia**: \n- Transferencia tecnología\n- Economías escala\n- Competencia mercado interno\n- Mejora estándares calidad",
                    "ied": "💼 **Inversión Extranjera Directa**: \n- Empresas maquiladoras\n- Clusters automotriz/aeroespacial\n- Servicios globales\n- Investigación y desarrollo",
                    "instituciones": "🏛️ **Fortaleza institucional**: \n- Reformas regulatorias\n- Transparencia procedimientos\n- Protección propiedad intelectual\n- Sistema judicial comercial",
                    "sostenibilidad": "🌱 **Desarrollo sostenible**: \n- Capítulos ambientales TLCs\n- Energías renovables\n- Economía circular\n- Responsabilidad social empresarial"
                }
            }
        }
    }
}

# Mensajes sorpresa expandidos
surprise_messages = [
    "💡 ¿Sabías que México fue el primer país de América Latina en firmar un TLC con países europeos (TLCUE en 2000)?",
    "🌟 El T-MEC incluye el capítulo laboral más avanzado de cualquier tratado comercial a nivel global",
    "📚 La Convención de Viena sobre Derecho de los Tratados tiene 116 estados parte y es considerada la 'constitución' del derecho treaty",
    "🌎 México tiene tratados comerciales con países que representan más del 60% del PIB mundial",
    "🚀 Las PYMEs mexicanas representan el 72% del empleo y 52% del PIB nacional",
    "🏛️ La OMA tiene 183 miembros que representan el 98% del comercio internacional mundial",
    "📊 México es el 2° socio comercial de Estados Unidos y el 1° para 6 estados de la unión americana",
    "🤝 El Centro de Comercio Internacional ha ayudado a más de 3 millones de mujeres empresarias a través de su iniciativa SheTrades"
]

# Menú principal
st.sidebar.title("Navegación Principal 🗺️")

# Sección de Unidades
st.sidebar.markdown("### 📖 Unidades de Aprendizaje")
unidad_seleccionada = st.sidebar.radio(
    "Selecciona una unidad:",
    ["Inicio 🏠"] + [f"{knowledge_base[unidad]['emoji']} {unidad.replace('_', ' ').title()}" 
                     for unidad in knowledge_base.keys()]
)

# Sección de Quiz separada
st.sidebar.markdown("---")
st.sidebar.markdown("### 🧠 Evaluación de Conocimientos")
if st.sidebar.button("Realizar Quiz 📝"):
    st.session_state.quiz_active = True

# Modo nocturno
st.sidebar.markdown("---")
modo_nocturno = st.sidebar.checkbox("Modo Nocturno 🌙")
if modo_nocturno:
    st.sidebar.info("💤 Recuerda: El descanso es importante para el aprendizaje efectivo. Estudia en intervalos de 45-50 minutos.")

# Mensaje sorpresa ocasional
st.sidebar.markdown("---")
if st.sidebar.button("Mensaje Sorpresa 🎁"):
    st.sidebar.success(random.choice(surprise_messages))

# Procesar selección de unidad
if unidad_seleccionada == "Inicio 🏠":
    col1, col2 = st.columns([2, 1])
    
    with col1:
        st.markdown("""
        ## ¡Bienvenido a Potro Internacional! 🐎
        
        **Tu asistente especializado en tratados y comercio internacional**
        
        ### 📚 Descripción del Curso
        
        Este curso analiza los tratados internacionales desde una perspectiva histórica, jurídica y económica, 
        con especial énfasis en la experiencia mexicana y su integración en la economía global.
        
        ### 🎯 Objetivos de Aprendizaje
        
        - Comprender la evolución histórica de los tratados internacionales
        - Analizar el marco jurídico de los acuerdos comerciales
        - Identificar oportunidades y amenazas para empresas mexicanas
        - Evaluar impactos económicos de la integración comercial
        
        ### 📖 Estructura del Contenido
        """)
        
        for unidad_key, unidad_data in knowledge_base.items():
            st.markdown(f"**{unidad_data['emoji']} {unidad_key.replace('_', ' ').title()}**")
            st.markdown(f"*{unidad_data['descripcion']}*")
            
    with col2:
        st.markdown("""
        ### ✨ Características Especiales
        
        🧠 **Quiz interactivo** para evaluar tu conocimiento  
        🌙 **Modo nocturno** con consejos de estudio  
        🎁 **Mensajes sorpresa** con datos curiosos  
        🔍 **Información detallada** con subtemas específicos  
        📊 **Datos actualizados** 2024  
        🌎 **Perspectiva global** con enfoque mexicano  
        
        ### 🚀 Tips de Estudio
        
        - Revisa una unidad por sesión
        - Toma notas de los conceptos clave
        - Practica con el quiz interactivo
        - Relaciona los conceptos con casos reales
        
        👈 **Selecciona una unidad en el menú lateral para comenzar!**
        """)
    
else:
    # Extraer unidad seleccionada
    unidad_key = [key for key in knowledge_base.keys() 
                 if knowledge_base[key]['emoji'] in unidad_seleccionada][0]
    unidad_data = knowledge_base[unidad_key]
    
    st.header(f"{unidad_data['emoji']} {unidad_seleccionada}")
    st.markdown(f"**{unidad_data['descripcion']}**")
    
    # Mostrar temas principales
    for tema_key, tema_data in unidad_data['temas'].items():
        with st.expander(f"{tema_data['emoji']} {tema_data['pregunta']}"):
            st.write(f"**{tema_data['respuesta']}**")
            
            # Mostrar subtemas si existen
            if 'subtemas' in tema_data:
                st.markdown("---")
                st.markdown("### 📋 Información Detallada")
                for subtema_key, subtema_text in tema_data['subtemas'].items():
                    # Extraer emoji y texto del subtema
                    subtema_emoji = subtema_text.split(' ')[0]
                    subtema_contenido = ' '.join(subtema_text.split(' ')[1:])
                    st.markdown(f"**{subtema_emoji} {subtema_key.replace('_', ' ').title()}**")
                    st.markdown(f"{subtema_contenido}")
                    st.markdown("")  # Espacio entre subtemas

# Sección de Quiz (solo se muestra cuando se activa)
if st.session_state.quiz_active:
    st.markdown("---")
    st.header("🧠 Quiz de Conocimientos - Tratados Internacionales")
    st.markdown("Evalúa tu comprensión de los conceptos clave del curso:")
    
    quiz_questions = {
        "¿Qué organización crea y actualiza los Incoterms regularmente?": {
            "options": ["Organización Mundial del Comercio (OMC)", "Cámara Internacional de Comercio (CCI)", "Organización Mundial de Aduanas (OMA)", "Naciones Unidas (ONU)"],
            "correct": "Cámara Internacional de Comercio (CCI)",
            "explicacion": "💼 La Cámara Internacional de Comercio crea y actualiza los Incoterms regularmente. La última versión son los Incoterms 2020."
        },
        "¿Cuál es el tratado comercial más importante para México en términos de volumen de comercio?": {
            "options": ["TLC con la Unión Europea", "T-MEC con Estados Unidos y Canadá", "Alianza del Pacífico", "ACE con Japón"],
            "correct": "T-MEC con Estados Unidos y Canadá", 
            "explicacion": "🇺🇸 El T-MEC representa más del 60% del comercio exterior total de México y es fundamental para la economía nacional."
        },
        "¿Qué establece principalmente la Convención de Viena de 1969?": {
            "options": ["Derecho internacional del mar", "Derecho de los tratados internacionales", "Derecho espacial internacional", "Derecho internacional ambiental"],
            "correct": "Derecho de los tratados internacionales",
            "explicacion": "🏛️ La Convención de Viena de 1969 codifica las normas consuetudinarias sobre celebración, aplicación y terminación de tratados entre Estados."
        },
        "¿Qué significa OMA y cuál es su principal función?": {
            "options": ["Organización Mundial del Azúcar - regular precios", "Organización Mundial de Aduanas - armonizar procedimientos aduaneros", "Organización Meteorológica Americana - pronósticos clima", "Oficina Mexicana Ambiental - protección ecológica"],
            "correct": "Organización Mundial de Aduanas - armonizar procedimientos aduaneros",
            "explicacion": "📦 La OMA (Organización Mundial de Aduanas) fue fundada en 1952 y su función principal es armonizar y facilitar los procedimientos aduaneros a nivel global."
        },
        "¿Qué principio de la OMC establece que un país no puede discriminar entre sus socios comerciales?": {
            "options": ["Trato nacional", "Nación más favorecida", "Transparencia", "Competencia leal"],
            "correct": "Nación más favorecida",
            "explicacion": "⚖️ El principio de Nación Más Favorecida (NMF) establece que cualquier ventaja concedida a un miembro de la OMC debe extenderse inmediatamente a todos los demás miembros."
        }
    }
    
    score = 0
    user_answers = {}
    
    for i, (pregunta, datos) in enumerate(quiz_questions.items()):
        st.markdown(f"**{i+1}. {pregunta}**")
        user_answer = st.radio(
            f"Selecciona tu respuesta:",
            datos["options"],
            key=f"q_{i}",
            index=None
        )
        user_answers[pregunta] = user_answer
        
        # Mostrar explicación inmediatamente si se seleccionó respuesta
        if user_answer:
            if user_answer == datos["correct"]:
                st.success(f"✅ **Correcto!** {datos['explicacion']}")
                score += 1
            else:
                st.error(f"❌ **Incorrecto.** {datos['explicacion']}")
        
        st.markdown("---")
    
    st.subheader(f"📊 Resultado Final: {score}/{len(quiz_questions)} respuestas correctas")
    
    if score == len(quiz_questions):
        st.balloons()
        st.success("🎉 ¡Excelente! Dominas los conceptos fundamentales del curso.")
    elif score >= len(quiz_questions) * 0.7:
        st.warning("👍 Buen trabajo, pero hay algunos conceptos que necesitas repasar.")
    else:
        st.error("📚 Es recomendable que revises los materiales del curso antes de continuar.")
    
    if st.button("Volver al menú principal 🏠"):
        st.session_state.quiz_active = False
        st.rerun()

# Pie de página
st.sidebar.markdown("---")
st.sidebar.markdown("### 📞 Soporte y Recursos")
st.sidebar.info("""
**Potro Internacional 🐎**  
*Tu compañero en comercio exterior*  
**Desarrollado para:** Curso de Tratados Internacionales  
**Fuentes principales:** Diapositivas del curso y bibliografía especializada  
**Actualizado:** Diciembre 2024
""")

# Información de contacto expandida
with st.sidebar.expander("ℹ️ Acerca de este chatbot"):
    st.markdown("""
    ### 🎯 Objetivo Educativo
    Facilitar el aprendizaje interactivo sobre tratados internacionales mediante:
    - Explicaciones claras y estructuradas
    - Ejemplos prácticos y casos reales
    - Evaluación formativa del conocimiento
    - Acceso inmediato a información relevante
    
    ### 📚 Fuentes Académicas
    - Programa Global del Curso
    - Diapositivas de todas las unidades
    - Bibliografía especializada en tratados
    - Datos oficiales de organismos internacionales
    
    ### 🐎 Potro Internacional 
    *Galopando hacia el conocimiento del comercio global*
    
    **¡Buen provecho en tu aprendizaje!**
    """)
