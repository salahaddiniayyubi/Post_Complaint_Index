---
title: "2024-cü İlin II Yarısı Üçün Poçt Operatorlarının Şikayət İndeksi"
author: "İCTA"
date: "`r format(Sys.Date(), '%d %B %Y')`"
bibliography: references.bib

output:
  pdf_document:
    latex_engine: lualatex
    fig_caption: yes
    number_sections: true
  html_document:
    df_print: paged
header-includes:
  - \usepackage{fontspec}
  - \setmainfont{Arial}
  - \usepackage{float}
  - \floatplacement{figure}{H}
  - \usepackage{hyperref}
  - \usepackage{longtable}
  - \usepackage{booktabs}
  - \usepackage{titling}
  - \usepackage{array}
  - \usepackage{tabularray}
  - \usepackage{xcolor}
  - \usepackage{colortbl}
  - \usepackage{multirow}
  - \usepackage{makecell}
  - \usepackage{tcolorbox}
  - \usepackage{tabularx}
  - \UseTblrLibrary{booktabs}
  - \AtBeginDocument{\let\maketitle\relax}
  - \usepackage{tikz}
  - \usetikzlibrary{calc}
  - \definecolor{mydarkblue}{RGB}{10,40,120}
  - \usepackage{graphicx}
---

\begin{titlepage}
    \begin{tikzpicture}[remember picture, overlay]
        % Draw a thick dark blue frame around the page
        \draw[line width=8pt, color=mydarkblue, rounded corners=28pt]
            ($(current page.north west) + (1.1cm,-1.1cm)$) rectangle
            ($(current page.south east) + (-1.1cm,1.1cm)$);
    \end{tikzpicture}
    \begin{center}
        \vspace*{1.5cm}
        % Logo (optional)
        \includegraphics[width=0.30\textwidth, keepaspectratio]{ikta.eps}
        
        \vspace{1.5cm}
        {\fontsize{26}{34}\selectfont\bfseries \textcolor{mydarkblue}{2024-cü İlin II Yarısı Üçün Poçt Operatorlarının Şikayət İndeksi}}\\[1.2em]
        {\fontsize{18}{24}\selectfont\bfseries \textcolor{black}{Analitik Hesabat}}\\[1.2em]
        {\fontsize{15}{20}\selectfont\bfseries \textcolor{mydarkblue}{İnformasiya Kommunikasiya Texnologiyaları Agentliyi (İKTA)}}\\[0.5em]
        {\fontsize{13}{18}\selectfont Azərbaycan Respublikasının Rəqəmsal İnkişaf və Nəqliyyat Nazirliyi}\\[1.5em]
        \vfill
        {\large Dərcolunma tarixi: \textbf{May 2025}}
    \end{center}
\end{titlepage}
\newpage

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE, warning = FALSE, message = FALSE, dev = "png", dpi = 300)
library(tidyverse)
library(readxl)
library(kableExtra)
library(ggthemes)
library(ggrepel)
library(DT)  # For interactive tables in HTML output
```



# Giriş

Azərbaycanda poçt xidmətləri sektorunun son illərdə dinamik inkişafı və bazarda yeni iştirakçıların meydana çıxması rəqabət mühitinin güclənməsinə və xidmət keyfiyyətinin yüksəlməsinə səbəb olmuşdur [@wik2009]. Bu proses, vətəndaşların məmnunluğunun artırılması və istifadəçi hüquqlarının qorunması baxımından dövlət siyasətinin əsas prioritetlərindən birinə çevrilmişdir. Müasir tənzimləmə yanaşmalarında poçt operatorlarının fəaliyyətinin şəffaf və obyektiv qiymətləndirilməsi, həmçinin xidmət keyfiyyətinin davamlı monitorinqi xüsusi əhəmiyyət kəsb edir [@azernews2019].

İnformasiya Kommunikasiya Texnologiyaları Agentliyi (İKTA) tərəfindən tətbiq edilən **Şikayət İndeksi** metodologiyası, poçt operatorlarının bazar payı ilə müqayisədə şikayət səviyyəsini obyektiv şəkildə ölçmək və sektorun şəffaflığını təmin etmək məqsədi daşıyır [@ofcom2023]. Bu indeks beynəlxalq tənzimləmə təcrübəsinə əsaslanaraq, operatorların performansının qiymətləndirilməsində və tənzimləyici tədbirlərin prioritetləşdirilməsində effektiv alət kimi çıxış edir [@wik2009; @azernews2019].

Hazırkı hesabatın əsas məqsədi aşağıdakılardır:

1. Poçt operatorlarının xidmət keyfiyyətinin qiymətləndirilməsi üçün beynəlxalq təcrübə və elmi əsaslara dayanan **Şikayət İndeksi** metodologiyasını hazırlamaq;
2. Poçt operatorlarının xidmət keyfiyyətini bazar payları ilə müqayisədə obyektiv qiymətləndirmək;
3. İstehlakçı məmnuniyyətini kəmiyyətləşdirən göstəricilər əsasında performans təhlili aparmaq.

İKTA tərəfindən "E-Şikayət" sisteminin təkmilləşdirilməsi və şikayətlərin elektron əsasda toplanması,
statistik təhlil imkanlarını genişləndirmiş və poçt sahəsində tənzimləmənin həyata keçirilməsi üçün yeni mərhələ yaratmışdır [@icta2009]. 
Lakin, poçt operatorlarının fəaliyyətinin obyektiv qiymətləndirilməsi üçün meyarlar işlənib hazırlanmamışdır. 
Bu hesabatda, poçt operatorları üçün beynəlxalq təcrübə və elmi əsaslara söykənən **Şikayət İndeksi** metodologiyası irəli sürülür. 
Bundan başqa, 2024-cü ilin ikinci yarısı üzrə Azərbaycanda fəaliyyət göstərən poçt operatorlarının  şikayət indeksi irəli sürülən metodologiya əsasında hesablanır və 
təhlil edilir, nəticələr isə həm cədvəl, həm də vizual formada ictimaiyyətə təqdim olunur.

# Metodologiya

## Şikayət İndeksinin Riyazi Əsasları

### Əsas Təriflər

1. **Bazar Payı (Market Share, $MS_i$):**

   Hər bir poçt operatorunun bazar payı ($MS_i$), həmin operatorun bazar göstəricisinin (cari halda, göndəriş sayı) bütün bazar üzrə ümumi göstəriciyə nisbəti kimi hesablanır. Bu göstərici operatorun ümumi bazarda tutduğu mövqeyi və fəaliyyətinin miqyasını obyektiv şəkildə əks etdirir.

   $$
   MS_i = \frac{S_i}{\displaystyle\sum_{j=1}^{n} S_j} \times 100\%
   $$

   Burada:
   - $MS_i$ - $i$-ci operatorun bazar payı (% ilə ifadə olunur);
   - $S_i$ - $i$-ci operatorun bazar göstəricisi (göndəriş sayı);
   - $n$ - ümumi operator sayı;
   - $i$ - ixtiyari $i$ operatoru;
   - $\sum_{j=1}^{n} S_j$ - bütün operatorların bazar göstəricilərinin cəmi.

   Bu yanaşma, operatorların bazardakı real çəkisini müqayisə etməyə şərait yaradır. Bazar payı yüksək olan operatorlar, ümumilikdə daha böyük istifadəçi bazasına və ya daha çox əməliyyata malik olurlar.


2. **Şikayət Payı (Complaint Share, $CS_i$):**

   Şikayət payı ($CS_i$), hər bir operatorun aldığı şikayətlərin ümumi şikayətlərin sayına nisbətini ifadə edir. Bu göstərici operatorun xidmət keyfiyyətinin və istifadəçi məmnuniyyətinin kəmiyyətcə qiymətləndirilməsində əsas rol oynayır. Yəni, bazarda fəaliyyət göstərən $n$ operator üçün $i$-ci operatorun şikayət payı aşağıdakı kimi hesablanır:

   $$
   CS_i = \frac{C_i}{\displaystyle\sum_{j=1}^{n} C_j} \times 100\%
   $$

   Burada:
   - $CS_i$ – $i$-ci operatorun şikayət payı (% ilə ifadə olunur);
   - $C_i$ – $i$-ci operatorla bağlı daxil olan şikayətlərin sayı;
   - $n$ – bazarda fəaliyyət göstərən operatorların ümumi sayı;
   - $\sum_{j=1}^{n} C_j$ – bütün operatorlarla bağlı daxil olan ümumi şikayət sayı.

   Şikayət payının yüksək olması, istifadəçi məmnuniyyətinin aşağı olduğunu və xidmət keyfiyyətinin təkmilləşdirilməsinə ehtiyac olduğunu göstərə bilər.


### İndeks Hesablanması

Şikayət İndeksi (Complaint Index) hər bir operator üçün, həmin operatorun şikayət payı ilə bazar payı arasındakı fərqi göstərir. Bu indeksin məqsədi, operatorun bazardakı mövqeyi ilə müqayisədə istifadəçi şikayətlərinin səviyyəsini obyektiv şəkildə qiymətləndirməkdir. İndeks aşağıdakı düsturla hesablanır:

$$
CI_i = CS_i - MS_i
$$

Burada:
- $CI_i$ - $i$-ci operatorun şikayət indeksi;
- $CS_i$ - $i$-ci operatorun şikayət payı (% ilə);
- $MS_i$ - $i$-ci operatorun bazar payı (% ilə).

**İndeksin interpretasiyası aşağıdakı kimidir:**

- $CI_i \leq -10\%$ - **Yüksək Performans** (yaşıl $\textcolor{green}{\large\textbullet}$): Operatorun şikayət payı bazar payından əhəmiyyətli dərəcədə azdır və bu, yüksək xidmət keyfiyyətinin göstəricisidir.
- $-10\% < CI_i < 10\%$ - **Qənaətbəxş Performans** (sarı $\textcolor{yellow}{\large\textbullet}$): Operatorun şikayət payı bazar payına yaxındır və xidmət keyfiyyəti qənaətbəxş hesab olunur.
- $CI_i \geq 10\%$ - **Zəif Performans** (qırmızı $\textcolor{red}{\large\textbullet}$): Operatorun şikayət payı bazar payından əhəmiyyətli dərəcədə çoxdur və bu, xidmət keyfiyyətinin aşağı olduğunu göstərir.

Bu yanaşma, müxtəlif ölçülü operatorlar arasında obyektiv müqayisə aparmağa imkan verir və tənzimləyici orqan üçün prioritet müdaxilə sahələrini müəyyənləşdirməkdə mühüm rol oynayır.


\begin{tcolorbox}[colback=green!10!white,colframe=green!80!black,title={Nümunə Hesablama}]
\textbf{AZƏRPOÇT} operatoru üçün:

\begin{align*}
S_i &= 4157 \qquad \sum S_j = 10,000 \\
MS_i &= \frac{4157}{10,000} \times 100\% = 41.57\% \\
C_i &= 119 \qquad \sum_{j=1}^{n} C_j = 337 \\
CS_i &= \frac{119}{\sum_{j=1}^{n} C_j} \times 100\% = \frac{119}{337} \times 100\% = 35.31\% \\
CI_i &= CS_i - MS_i = 35.31\% - 41.57\% = -6.26\%
\end{align*}

\textbf{Nəticə:} Qənaətbəxş Performans (Sarı zonada - $\textcolor{yellow}{\large\textbullet}$)
\end{tcolorbox}

### Niyə Bazar Payı Gözlənilən Şikayət Səviyyəsi üçün Əsas Kimi Seçilir?

Şikayət indeksinin hesablanmasında bazar payının istifadə olunmasının əsas səbəbi, hər bir operatorun bazardakı real miqyasını və istifadəçi bazasının böyüklüyünü nəzərə almaqdır. Bazar payı, operatorun ümumi bazar daxilində tutduğu mövqeyi və xidmət etdiyi müştəri sayını əks etdirir. Prinsip etibarilə, operatorun bazar payı nə qədər böyükdürsə, həmin operatorun daha çox istifadəçi ilə qarşılıqlı əlaqədə olması və nəticədə daha çox şikayət alma ehtimalı da bir o qədər yüksəkdir.

Başqa sözlə, bazar payı operator üçün **gözlənilən şikayətlərin intensivliyinin** təbii ölçüsüdür. Əgər bütün operatorlar eyni xidmət keyfiyyətinə malik olsaydı, onların şikayət payları bazar payları ilə proporsional olardı. Məsələn, bazarın 40%-ni əhatə edən operatorun bütün şikayətlərin də təxminən 40%-ni alması gözləniləndir. Bu yanaşma, operatorların fərqli ölçüdə olması və istifadəçi bazasının müxtəlifliyi şəraitində obyektiv müqayisə aparmağa imkan verir.

Əgər bir operatorun faktiki şikayət payı bazar payından xeyli çoxdursa, bu, həmin operatorun xidmət keyfiyyətində problemlərin olduğunu və istifadəçi narazılığının yüksək səviyyədə olduğunu göstərir. Əksinə, faktiki şikayət payı bazar payından az olan operatorlar isə, xidmət keyfiyyətinin və istifadəçi məmnuniyyətinin yüksək olduğunu nümayiş etdirir.

Bu metodologiya beynəlxalq tənzimləmə təcrübəsində də istifadə olunan prinsiplərə əsaslanır. 
Belə ki, Universal Postal Union (UPU), Ofcom (Birləşmiş Krallıq), və ERGP (Avropa Poçt Tənzimləyiciləri Qrupu) kimi qurumlar şikayətlərin və performans göstəricilərinin operatorun bazar payı və ya xidmət həcmi ilə nisbətdə qiymətləndirilməsini tövsiyə edirlər [@upu2022; @ofcom2023; @ergp2022]. 
Lakin, bu hesabatda tətbiq olunan **şikayət indeksi** (faktiki şikayət payı ilə bazar payı arasındakı fərq) mövcud beynəlxalq yanaşmaların modifikasiya etdirilmiş formasıdır və 
operatorlar arasında obyektiv müqayisə aparmaq üçün daha aydın və interpretasiya oluna bilən nəticə verir. Cari indeks -100 və 100 arasında dəyişir.

Beləliklə, bazar payı şikayətlərin gözlənilən səviyyəsini müəyyən etmək üçün əsas baza kimi çıxış edir və bu indeksin hesablanması ədalətli müqayisə imkanı yaradır.

# 2024-cü İlin II Yarısı Üçün Poçt Operatorları Üçün Şikayət İndeksinin Hesablanması

## Məlumatlar və Onlar Əsasında Hesablanmış Şikayət İndeksi

Cədvəl \ref{tab:complaint-index-table}-də, 2024-cü ilin ikinci yarısı üzrə Azərbaycanda fəaliyyət göstərən əsas poçt operatorlarının şikayət indeksləri təqdim olunur. Hər bir operator üçün bazar payı, daxil olan şikayətlərin sayı, həmin şikayətlərin ümumi şikayətlərdəki payı, gözlənilən şikayət payı (bazar payına əsaslanan) və nəticədə əldə olunan şikayət indeksi göstərilib.

Cədvəldə diqqət çəkən əsas məqamlar aşağıdakılardır:

- **LIMAK AZ** operatoru 2.37\% bazar payına malik olmasına baxmayaraq, ümumi şikayətlərin 12.76\%-ni alıb və şikayət indeksi 10.39 olaraq ən yüksək səviyyədədir. Bu, operatorun xidmət keyfiyyətində ciddi problemlərin olduğunu göstərir və "Zəif" qiymətləndirilib.
- Digər operatorların əksəriyyəti üçün şikayət indeksi 10\%-dən aşağıdır və onlar "Qənaətbəxş" kateqoriyasında yer alır. Bu, onların şikayət səviyyəsinin bazar payı ilə nisbətən uyğun olduğunu göstərir.
- **AZƏRPOÇT** operatoru isə ən böyük bazar payına (41.57\%) malik olsa da, şikayət indeksi mənfi (-6.26) olub, bu operatorun şikayət səviyyəsinin bazar payından aşağı olduğunu və xidmət keyfiyyətinin qənaətbəxş olduğunu göstərir.

Ümumilikdə, cədvəl operatorlar arasında xidmət keyfiyyəti və istifadəçi məmnuniyyəti baxımından obyektiv müqayisə aparmağa imkan verir. 
Şikayət indeksi yüksək olan operatorlar üçün əlavə tənzimləyici tədbirlərin görülməsi məqsədəuyğun hesab olunur.


```{r data-processing}
# DATA MERGE (REAL EXAMPLE FROM YOUR FILES)
market <- read_excel("./data/marketshare_2024_2.xlsx") %>%
  select(Operator = `Operator`, Market_Share = `Bazar Payı`) %>%
  mutate(Operator = str_remove_all(Operator, '"|"|MMC|QSC|PHŞ|ASC')) %>%
  slice(1:(nrow(.) - 3))

complaints <- read_excel("./data/complaints_2024_2.xlsx") %>% 
  select(Operator = `Provayder`, Complaints = `Şikayət Sayı`) %>%
  mutate(Operator = str_remove_all(Operator, '\"|\"|MMC|QSC|PHŞ|ASC')) %>%
  slice(1:(nrow(.) - 3))

merged <- full_join(market, complaints, by = "Operator") %>%
  mutate(Complaints = replace_na(Complaints, 0)) %>%
  filter(Operator != "Total") %>%
  filter(!str_detect(tolower(Operator), "applied filters")) %>%
  mutate(
    Total_Complaints = sum(Complaints),
    Complaint_Share = (Complaints/Total_Complaints)*100,
    Expected_Share = Market_Share*100,
    Complaint_Index = Complaint_Share - Expected_Share,
    Performance = case_when(
      Complaint_Index >= 10 ~ "Zəif (#FF6B6B)",
      between(Complaint_Index, -10, 10) ~ "Qənaətbəxş (#FFE66D)",
      Complaint_Index <= -10 ~ "Yüksək (#6BFF97)"
    )
  )
```





```{r table, results='asis'}

library(dplyr)
library(stringr)
library(kableExtra)

filtered_df <- merged %>%
  filter(Market_Share > 0, Complaint_Share > 0) %>%
  select(
    Operator, Market_Share, Complaints, Complaint_Share, Expected_Share, Complaint_Index, Performance
  ) %>%
  arrange(desc(Market_Share)) %>%
  mutate(
    Market_Share = round(Market_Share*100, 2),
    Complaint_Share = round(Complaint_Share, 2),
    Expected_Share = round(Expected_Share, 2),
    Complaint_Index = round(Complaint_Index, 2)
  ) %>%
  rename(
    "Operator" = Operator,
    "Bazar Payı (%)" = Market_Share,
    "Şikayət Sayı" = Complaints,
    "Həqiqi Şikayət Payı (%)" = Complaint_Share,
    "Gözlənilən Şikayət Payı (%)" = Expected_Share,
    "Şikayət İndeksi" = Complaint_Index,
    "Qiymətləndirmə" = Performance
  )
# Remove color codes from Performance
filtered_df$Qiymətləndirmə <- stringr::str_remove(filtered_df$Qiymətləndirmə, " \\(#?[A-Fa-f0-9]{6}\\)")


kableExtra::kable(filtered_df, booktabs = TRUE, caption = "\\label{tab:complaint-index-table}{Poçt Operatorlarının Şikayət İndeksi}", escape = TRUE) %>%
  kableExtra::kable_styling(
    latex_options = c("striped", "hold_position", "scale_down"),
    font_size = 9,
    full_width = FALSE,
    position = "center"
  ) %>%
  kableExtra::column_spec(1, width = "2cm") %>%  # Adjust widths manually
  kableExtra::column_spec(2, width = "2cm") %>%
  kableExtra::column_spec(3, width = "2cm") %>%
  kableExtra::column_spec(4, width = "2cm") %>%
  kableExtra::column_spec(5, width = "2cm") %>%
  kableExtra::column_spec(6, width = "2cm") %>%
  kableExtra::add_footnote(
    "Qeyd: Bazar payı 0.1%-dən az olan operatorlar çertyojda göstərilməyib",
    notation = "symbol"
  )

```

## Vizual Təhlil
Aşağıdakı qrafikdə hər bir operator üçün gözlənilən şikayət payı (bazar payı əsasında) və faktiki (həqiqi) şikayət payı müqayisə edilir. Diaqramda hər bir nöqtə bir operatoru təmsil edir; nöqtənin ölçüsü operatorun aldığı şikayətlərin sayını, rəngi isə qiymətləndirmə kateqoriyasını (məsələn, "Zəif", "Qənaətbəxş") göstərir.

- Qrafikdə diaqonal (45 dərəcə) xətt gözlənilən və faktiki şikayət paylarının bərabər olduğu vəziyyəti göstərir. Bu xəttin üzərində və ya yaxınında yerləşən operatorlar şikayət səviyyəsi baxımından bazar payına uyğun nəticə göstərir.
- Diaqonalın yuxarısında yerləşən operatorlar (məsələn, LIMAK AZ) faktiki şikayət payı gözləniləndən xeyli yüksək olanlardır və bu, xidmət keyfiyyətində problemlərə işarədir.
- Diaqonalın aşağısında yerləşən operatorlar isə faktiki şikayət payı gözləniləndən az olanlardır və bu, daha yüksək xidmət keyfiyyətini göstərir.

Bu vizual analiz operatorlar arasında xidmət keyfiyyəti və istifadəçi məmnuniyyəti baxımından fərqləri aydın şəkildə nümayiş etdirir və tənzimləyici orqan üçün prioritet müdaxilə sahələrini müəyyənləşdirməkdə kömək edir.

```{r plot, fig.cap="Gözlənilən vs Həqiqi Şikayət Payı", fig.width=10, fig.height=6, dpi = 500}
# Filter data for plot
# Add Performance category column
plot_data <- merged %>% 
  filter(Market_Share >= 0.001, Complaint_Share >= 0.001) %>%
  mutate(Complaint_Index = Complaint_Share - Expected_Share,
         Performance = case_when(
           Complaint_Index >= 10 ~ "Zəif",
           Complaint_Index <= -10 ~ "Yüksək",
           TRUE ~ "Qənaətbəxş"
         ))

# VISUALIZATION CODE
ggplot(plot_data, aes(x = Expected_Share, y = Complaint_Share)) +
  geom_point(aes(size = Complaints, fill = Performance), shape = 21) +
  scale_fill_manual(values = c(
    "Yüksək" = "#6BFF97",        # Green for good performance
    "Qənaətbəxş" = "#FFE66D",    # Yellow for satisfactory
    "Zəif" = "#FF6B6B"           # Red for poor performance
  )) +
  scale_size_continuous(range = c(3, 12)) +
  geom_abline(slope = 1, intercept = 0, linetype = "dashed", color = "gray") +
  geom_text_repel(aes(label = Operator), size = 3, max.overlaps = Inf) +
  labs(title = "Gözlənilən və Faktiki Şikayət Payı (Loqarifmik Ölçüdə)",
      #  subtitle = "Log-log scale comparison of expected and actual complaint shares",
       x = "Gözlənilən Şikayət Payı (%)",
       y = "Faktiki Şikayət Payı (%)",
       size = "Şikayət Sayı",
       fill = "Qiymətləndirmə") +
  scale_y_log10(labels = scales::percent_format(scale = 1)) +
  scale_x_log10(labels = scales::percent_format(scale = 1)) +
  theme_light() +
theme(
  legend.box = "vertical",  # Place legends vertically
  legend.box.background = element_rect(color = "black", size = 0.5, fill = "white"),
  legend.box.margin = margin(10, 10, 10, 10),
  legend.title = element_text(face = "bold", size = 12),
  legend.text = element_text(size = 10),
  axis.text.x = element_text(face = "bold"),
  axis.text.y = element_text(face = "bold"),
  legend.position = "right"
) +
guides(
  fill = guide_legend(
    title = "Qiymətləndirmə",
    override.aes = list(size = 8, shape = 21, color = "black"),
    label.position = "bottom",
    title.position = "top",
    title.theme = element_text(face = "bold", size = 12)
  ),
  size = guide_legend(
    title = "Şikayət Sayı",
    override.aes = list(shape = 21, fill = "gray90", color = "black"),
    label.position = "bottom",
    title.position = "top",
    title.theme = element_text(face = "bold", size = 12)
  )
)


```


# Nəticə

Bu hesabatda poçt operatorlarının fəaliyyətinin obyektiv və şəffaf qiymətləndirilməsi üçün beynəlxalq təcrübəyə və elmi əsaslara söykənən Şikayət İndeksi metodologiyası təqdim olundu. Hesablamalar göstərdi ki, şikayətlərin bazar payı ilə müqayisədə təhlili operatorlar arasında xidmət keyfiyyəti və istifadəçi məmnuniyyəti baxımından obyektiv müqayisə aparmağa imkan verir. 

2024-cü ilin ikinci yarısına dair məlumatların təhlili göstərdi ki, bəzi operatorlar (məsələn, LIMAK AZ) bazar payına nisbətən daha çox şikayət alaraq "zəif" kateqoriyasında yer alıb, əksər operatorlar isə "qənaətbəxş" səviyyədə performans göstərmişdir. Ən böyük bazar payına malik olan AZƏRPOÇT-un şikayət indeksi isə mənfi olmuş və bu operatorun xidmət keyfiyyətinin ümumilikdə qənaətbəxş olduğunu göstərmişdir (bax: Cədvəl 1 və Şəkil 1).

Təklif olunan metodologiya tənzimləyici orqan üçün prioritet müdaxilə sahələrinin müəyyənləşdirilməsində, istifadəçi hüquqlarının qorunmasında və sektorun davamlı inkişafında mühüm rol oynayır. Şikayət indeksi yüksək olan operatorlar üçün xidmət keyfiyyətinin artırılması istiqamətində əlavə tədbirlərin görülməsi tövsiyə olunur. Eyni zamanda, bu yanaşma sektor üzrə şəffaflığın və ictimai hesabatlılığın artırılmasına xidmət edir.

Gələcəkdə şikayət indeksinin dinamikası üzrə davamlı monitorinqin aparılması, metodologiyanın daha da təkmilləşdirilməsi və beynəlxalq təcrübənin izlənməsi məqsədəuyğun hesab olunur. Bu, həm poçt operatorlarının rəqabət qabiliyyətinin artırılmasına, həm də vətəndaş məmnuniyyətinin davamlı yüksəldilməsinə töhfə verəcəkdir.


```{r interactive-table}
# Only run this in HTML output mode
if (knitr::is_html_output()) {
  merged %>%
    select(Operator, Market_Share, Complaints, Complaint_Share, Expected_Share, Complaint_Index, Performance) %>%
    mutate(
      Market_Share = round(Market_Share*100, 2),
      Complaint_Share = round(Complaint_Share, 2),
      Expected_Share = round(Expected_Share, 2),
      Complaint_Index = round(Complaint_Index, 2)
    ) %>%
    rename(
      "Operator" = Operator,
      "Bazar Payı (%)" = Market_Share,
      "Şikayət Sayı" = Complaints,
      "Həqiqi Şikayət Payı (%)" = Complaint_Share,
      "Gözlənilən Şikayət Payı (%)" = Expected_Share,
      "Şikayət İndeksi" = Complaint_Index,
      "Qiymətləndirmə" = Performance
    ) %>%
    datatable(
      options = list(
        pageLength = 10,
        language = list(
          search = "Axtar:",
          lengthMenu = "Göstər _MENU_ qeyd",
          info = "_TOTAL_ qeydindən _START_ - _END_ arası göstərilir",
          paginate = list(previous = "Əvvəlki", `next` = "Növbəti")
        )
      ),
      rownames = FALSE
    ) %>%
    formatStyle(
      'Qiymətləndirmə',
      color = styleEqual(
        c("Zəif (#FF6B6B)", "Qənaətbəxş (#FFE66D)", "Yüksək (#6BFF97)"),
        c("#FF6B6B", "#FFE66D", "#6BFF97")
      )
    )
}
```


# Ədəbiyyat
