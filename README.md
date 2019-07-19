
#  Welcome to MultiParametricMRI 

## Introduction
In this analysis, I did my best to explore the relationship between MR parameters derived from regions of interest that corresponded to image-guided tissue samples and their pathological diagnosis. This is all in an attempt to avoid the complications of tissue heterogeneity and the coexistence of treatment-induced injury and recurrent glioma within the same patient. 

## Organization
In this analysis, there were many moving parts. I had to write a lot of software to get my pipelines to work smoothly and ensure that I had the most representative data for my cohorts. Many of the pre-processing steps to ensure the resolution of my ROIs were the same as my images are not recorded here, but are found in my other github repo for preop processing. This analysis focuses on agglomerating the generated data, and analyzing it. I have broken down my analysis into 5 categories: 

 [GetMergeData](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData) 
 [QCData](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData) 
 [AnnotateData](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnnotateData) 
 [AnalyzeData](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData) 

These are the order in which I proceed through the analysis.

## GetMergeData
### Download pathology reports from database, place them into the same folder of interest
In our case we’re working with both new and old data, and these are our two datasets; therefore we have two folders called *   [Get_Old_P01](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_Old_P01) 
and  [Get_REC_HGG_Data](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_REC_HGG_Data) . 
### Creating list of old and new data: 
These can be found inside each of the folders above. 
[Creating_OldP01_BnumTnumList.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_Old_P01/Creating_OldP01_BnumTnumList.ipynb)  and  [Creating_REC_HGG_BnumTnumList.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_REC_HGG_Data/Creating_REC_HGG_BnumTnumList.ipynb) 
These create  [rec_hgg_process_list.79.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_REC_HGG_Data/rec_hgg_process_list.79.csv)  and  [po1_preop_recur_process_list.125.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_Old_P01/po1_preop_recur_process_list.125.csv) . 
### Using the commands in Scripts to agglomerate the data: 
 [Scripts](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Scripts)  
* Use the  [get_diffu1000_biopsy_data.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Scripts/get_diffu1000_biopsy_data.ipynb)  and 2000 version to get diffusion data; wasn’t working for me otherwise. 
* Use the  [get_old_data_spec.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Scripts/get_old_data_spec.ipynb)  to get spec data
* Use Logfile in Scripts directory to see scripts run to generate the data 
### Merge all old data together, as well as all new data together, then merge old with new
- Use  [OldDataMerge.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_Old_P01/OldDataMerge.ipynb) , creates  [old_po1_data.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_Old_P01/old_po1_data.csv) 
- Use  [NewDataMerge.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_REC_HGG_Data/NewDataMerge.ipynb) , creates  [rec_hgg_data.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Get_REC_HGG_Data/rec_hgg_data.csv) 
- Then use  [Merge_Data.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/Merge_Data.ipynb) , creates  [final_mri_with_path.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/GetMergeData/final_mri_with_path.csv) 

## QCData
### Write QC lists for manually looking at the placement of each tissue sample 
-  Use [WriteQCLists.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/QC_list_generation/WriteQCLists.ipynb) 
- Creates list of 10 scans at a time to look at each. 
- Use [batch_firsta_valid.py](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/batch_firsta_valid.py)  (example can be found in above notebook) to manually QC each sample and annotate whether inside a hematoma (based off perfusion)
### Result agglomeration
- The results go in  [QC_output_perf_po1_preop_recur](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/QC_output_perf_po1_preop_recur) ,  [QC_output_perf_REC_HGG](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/QC_output_perf_REC_HGG) , and then  [QC_Output_Agglomeration.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/QC_Output_Agglomeration.ipynb)  is used to agglomerate the results into something usable. Output is  [final_biopsy_qc.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/final_biopsy_qc.csv) 
## AnnotateData
1. Use  [AnnotateData.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnnotateData/AnnotateData.ipynb)  to ensure that all things that need to be removed based on [final_biopsy_qc.csv](http://localhost:8888/edit/home/sf673542/MultiParametricMRI/MP_MRI_Final/QCData/final_biopsy_qc.csv)  are removed
2. Combine lactate and lipid columns 
3. Read in pathology comments for outcome determination
4. Substitute values that weren’t calculated correctly and ended up as 0’s for NAs, annotate these substitutions. (so as not to mess up mean/median calculations)
5. Create columns that represent whether a certain sample has or doesn’t have a certain modality. 
6. Substitute diffusion values derived from a gradient of b=2000 are so similar to the values derived from b=1000, we substitute those values in for b=1000 and annotate that
7. Annotate whether to include histology or not 
8. Create our outcome based on the pathological findings; a sample was considered “treatment effect” if it had no tumor cells, no serious necrosis, and if one of the following criteria were met: 1) a comment related to gliosis was present in the pathology comments; 2) treatment-related abnormal blood vessels were annotated; 3) if its clinical histology was deemed “treatment effect” at the time of surgery. 
9. Annotate whether the biopsy was in the contrast-enhancing lesion (CEL) or the non-enhancing lesion (NEL). 
10. Parses down things that should be excluded from analysis. 

## AnalyzeData
1.   [CEL_analysis](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData/CEL_analysis)  and  [NEL_analysis](http://localhost:8888/tree/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData/NEL_analysis)  hold  [NEL_Stats.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData/NEL_analysis/NEL_Stats.ipynb)  and  [CEL_Stats.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData/CEL_analysis/CEL_Stats.ipynb) , where the GEE analysis was performed to assess association between MR parameters and outcome
2. Then, threshold analysis was performed in  [CV_Thresh_LR.ipynb](http://localhost:8888/notebooks/home/sf673542/MultiParametricMRI/MP_MRI_Final/AnalyzeData/ML_TxEvsrHGG/CV_Thresh_LR.ipynb) 
3. Finally 






