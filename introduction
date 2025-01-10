对蝙蝠和蚊虫等病毒宿主进行表达谱分析
# 相关软件  
| 软件名称    | 功能描述                                                                 |
|-------------|--------------------------------------------------------------------------|
| STAR     | 将测序Reads与参考基因组进行比对的软件                                              |
| RSEM    | 从RNA-Seq数据中定量估计基因和转录本表达水平                     |

# task1 WDL流程开发
1.STAR建立索引、比对

2.RSEM构建索引、定量
![image](/uploads/53aa4e129fd2ea0dd79169534173cb5e/image.png)

## 1.1 STAR构建索引
原理：使用 STAR 软件为参考基因组构建索引，以便进行高效的比对和转录组分析。

输入：参考基因组文件（reference_genome）、注释文件（annotation_file）

输出：STAR 索引文件目录（instar）

## 1.2 STAR比对
原理：使用 STAR 将原始的 FASTQ 文件比对到参考基因组上，生成对齐的 BAM 文件。

输入：FASTQ 文件对（fastq1, fastq2）、STAR 索引文件（instar）

输出：基因组对齐 BAM 文件（genome_bam_file）、转录组对齐 BAM 文件（transcriptome_bam_file）

## 2.1 RSEM构建索引
原理：使用 RSEM 为参考基因组和注释文件构建转录本定量分析所需的索引，以便后续的表达量计算。

输入：参考基因组文件（reference_genome）、注释文件（annotation_file）

输出：RSEM 索引文件目录（inrsem）

## 2.2 RSEM转录本定量
原理：使用 RSEM 计算转录本的表达量，基于 STAR 生成的转录组 BAM 文件，输出基因和转录本的表达结果。

输入：转录组 BAM 文件（transcriptome_bam_file）、RSEM 索引文件（rsem_index_files）

输出：基因表达结果文件（gene_expression_results）、转录本表达结果文件（transcriptome_expression_results）

# 输入与输出
## 输入
![image](uploads/8f21aa02de9b42c230c376d103252c89/image.png){width=1278 height=287}
| 文件类型    | 描述                                                                 |
|-------------|--------------------------------------------------------------------------|
| fastq1_files     | 测序数据fastq1                   |
| fastq2_files    | 测序数据fastq2                    |
| reference_genome     | 参考基因组(fna)                     |
| annotation_file    | 基因组注释文件(gtf)                   |
## 测试数据
![image](uploads/4ebc0b013b08a079ed10fba880026f15/image.png){width=238 height=138}

/jdfssz1/ST_HEALTH/P20Z10200N0206/mixinrui/project/Upp/filterassembly/240423/pathlist里Pipistrellus_kuhlii蝙蝠的随机两个样本、及相应参考基因组和注释文件

## 输出
![image](uploads/39eb76ba36f90dcb8fe2dd26a2916536/image.png){width=1284 height=401}
| 文件类型    | 描述                                                                 |
|-------------|--------------------------------------------------------------------------|
| transcriptome_bam_files     | STAR比对后的转录组bam文件                                          |
| genome_bam_files    | STAR比对后的基因组bam文件                     |
| gene_expression_results     | RSEM定量后的基因表达结果                    |
| transcriptome_expression_results    | RSEM定量后的转录本表达结果                 |

## github参考文档
https://github.com/siyingwu29/HEPA
## 云平台地址
https://cloud.stomics.tech/#/project-management/P20Z10200N0206/workflow/workflow/detail?id=66b45aeea015b326032a4404&type=private&jumpType=workflow&version=Version.1.0.0&isPublic=private&fromProjectId=P20Z10200N0206&origin=&hasInToolbox=false
