# Grand Challenge in ACMMM 2024: Multilingual Medical Instructional Video Question Answering
The medical instructional video question answering aims at performing the temporal answer grounding task given a medical-related question in a single video or the video corpus. Those videos are collected from high-quality bilingual medical [Youtube](https://www.youtube.com/) channels and annotated by medical experts.

## Table of Contents
- [Background](#background)
- [Task Overview](#task_overview)
  - [Track 1. Multilingual Temporal Answer Grounding in Singe Video (mTAGSV)](#track1)
  - [Track 2. Multilingual Video Corpus Retrieval (mVCR)](#track2)
  - [Track 3. Multilingual Temporal Answer Grounding in Video Corpus (mTAGVC)](#track3)
- [Dataset](#dataset)
- [Evaluation](#evaluation)
- [Participation](#participation)
- [Award](#award)
- [Important Dates](#important_dates)
- [Reference](#reference)

## Background 
Recently, the availability of online videos has revolutionized the way to access information or gain knowledge [1]-[2]. Many people find instructional videos to be an effective and efficient way to teach or learn how to accomplish a particular task with a series of step-by-step procedures [3]-[4]. To this end, a new task temporal answer grounding in the Medical instructional video (TAGV) is proposed to find the video frame span corresponding to an input question. The ultimate goal for this shared task is to develop a system that can provide temporal answer video segments for the first-aid, medical emergency, or medical education.
## <a id="task_overview">Task Overview</a>
This shared task includes three tracks: Multilingual Temporal Answer Grounding in Singe Video (mTAGSV), Multilingual Video Corpus Retrieval (mVCR) and Multilingual Temporal Answer Grounding in Video Corpus (mTAGVC).

<div align=center>
<img src="./img/pic1.png" width="100%">
</div>
<div align ='center'>
<b>Fig. 1: Illustration of Multilingual Temporal Answer Grounding in Singe Video (mTAGSV).</b></a>
</div>


* <span id = "track1">**Track 1. Multilingual Temporal Answer Grounding in Singe Video (mTAGSV)**</span>: As shown in Fig. 1: given a medical or health-related question and a single untrimmed medical instructional video, this track aims to locate the temporal answer (start and end time points) within the video.



<div align=center>
<img src="./img/pic2.png" width="100%">
</div>
<div align ='center'>
<b>Fig. 2: Illustration of Multilingual Video Corpus Retrieval (mVCR).</b></a>
</div>



* <span id = "track2">**Track 2. Multilingual Video Corpus Retrieval (mVCR)**</span>: As shown in Fig. 2, given a medical or health-related question and a large collection of untrimmed medical instructional videos, this track aims to find the most relevant video corresponding to the given question in the video corpus.

<div align=center>
<img src="./img/pic3.png" width="100%">
</div>
<div align ='center'>
<b>Fig. 3: Illustration of Multilingual Temporal Answer Grounding in Video Corpus (mTAGVC).</b></a>
</div>



* <span id = "track3">**Track 3. Multilingual Temporal Answer Grounding in Video Corpus (mTAGVC)**</span>: As shown in Fig. 3, given a text question and a large collection of untrimmed medical instructional videos, this track aims at finding the matching video answer span within the most relevant video corresponding to the given question in the video corpus.
## Dataset 
<div align=center>
<img src="./img/pic4.png" width="60%">
</div>
<div align ='center'>
<b>Fig. 4: Dataset examples of the mTAGV shared task.</b></a>
</div>


The videos for this competition are crawled from the medical instructional channels on the YouTube website, where the subtitles (in Chinese and English) are transcribed from the corresponding video. The frames from the videos have been down-sampled to 16fps. The question and corresponding temporal answer are manually labeled by annotators with the medical background. Each video may contain several questions-answer pairs, where the questions with the same semantic meanings correspond to a unique answer. The dataset is split into a training set, a validation set, and a test set. During the grand challenge, the test set along with the true “id” data number is not available to the public. The Fig. 4 shows the dataset examples for the mTAGV shared task. The “id” is the sample number that is used for the video retrieval track. The “video_id” means the unique ID from YouTube. The “Chinese_question” item is written manually by Chinese medical experts. The “English_question” is translated and corrected by native English-speaking doctors. The “start and end second” represents the temporal answer from the corresponding video. We also provide the video captions automatically generated from the video, including Chinese (Ch_caption) and English (Eng_caption) versions. As a result, our final goal is to retrieve the target video ID from the test corpus, and then locate the visual answer.


## Evaluation
#### Track 1:
##### Multilingual Temporal Answer Grounding in Singe Video
We will evaluate the results using the metric calculation equation shown as follows. Specifically, we use (1) Intersection over Union (IoU), and (2) mIoU which is the average IoU over all testing samples. Following the previous work [3]-[5], we adopt “R@n, IoU = μ”, and “mIoU” as the evaluation metrics, which treat localization of the frames in the video as a span prediction task. The “R@n, IoU = μ” denotes the Intersection over Union (IoU) of the predicted temporal answer span compared with the ground truth span, where the overlapping part is larger than “μ” in top-n retrieved moments. The “mIoU” is the average IoU over the samples. In our experiments, we use n = 1 and μ ∈ {0.3, 0.5, 0.7} to evaluate the TAGSV results. 

$$
\begin{aligned}
 \mathrm{IOU} & =\frac{A \cap B}{A \cup B}  \\
\mathrm{mIOU} & =\left(\sum_{i=1}^n \mathrm{IOU}\right) / n
\end{aligned}
$$

where A and B represent different spans. 
</br>
**Note:** The main ranking of this track is based on the mIoU score, and other metrics in this track are also provided for further analysis.

#### Track 2:

##### Multilingual Video Corpus Retrieval 
Following the pioneering work [6], we adopt the video retrieval metric like “R@n”. Specifically, we adopt the n=1, 10, and 100 to denote the recall performance of the video retrieval. The Mean Reciprocal Rank (MRR) score to evaluate the Chinese medical instructional video corpus retrieval track, which can be calculated as follows.

$$
M R R=\frac{1}{|V|} \sum_{i=1}^{|V|} \frac{1}{{Rank}_i} 
$$

where the |*V*| is the number of the video corpus. For each testing sample *V*<sub>i</sub>, the Rank<sub>i</sub> is the position of the target ground-truth video in the predicted list.
</br>
**Note:** The main ranking of this track is based on the Overall score. The Overall score is calculated by averaging the R@1, R@10, R@100 and MRR scores, which is shown as follows.

$$
\text { Overall }=\frac{1}{|M|} \sum_{i=1}^{|M|} \frac{1}{\text { Value}_i}
$$

where the |*M*| is the number of the evaluation metrics. Value<sub>i</sub> is the i-th metric in the above metrics (R@1, R@10, R@100 and MRR), |M|=4.
#### Track 3:

##### Multilingual Temporal Answer Grounding in Video Corpus
We kept the Intersection over Union (IoU) metric similar to the Track 1 and the retrieval indexes “R@n, n=1/10/100” and MRR similar to Track 2 for further analysis. The “R@n, IoU = 0.3/0.5/0.7” is still used, where we assign the n = 1, 10, 100 for evaluation. The index of mean IoU in video retrieval subtask, i.e., “R@1/10/100|mIOU”, is also adopted for measuring the average level of participating model’s performance. 
</br>
**Note:** The main ranking of this track is based on the Average score. The Average score is calculated by averaging the R@1|mIoU, R@10|mIoU, R@100|mIoU scores, which is shown as follows.

$$
\text { Average }=\frac{1}{|M'|} \sum_{i=1}^{|M'|} \frac{1}{\text { Value}_i}
$$

where the |M<sup>'</sup>| is the number of the evaluation metrics. Value<sub>i</sub> is the value of the i-th metric (i.e., R@1|mIoU, R@10|mIoU, R@100|mIoU), |M<sup>'</sup>|=3.

## Participation
If you are interested in our challenge, please fill out the [application form]([http://tcci.ccf.org.cn/conference/2023/dldoc/NLPCC2023.SharedTask5.RegistrationForm.doc])(https://github.com/Lireanstar/ACMMM2024_MMIVQA/blob/main/ACMMM%202024%20MMIVQA%20Grand%20Challenge%20Agreement.docx) and email libinincn@hnu.edu.cn (Please email us with your organization's email and note that you participate in the challenge). The dataset will be sent to you by then. 

## <a id="important_dates"> Important Dates</a>
Announcement of shared tasks and call for participation:	2024/3/15

- [ ] Registration open:	2024/3/15
- [ ] Release of detailed task guidelines & training data:	2024/4/3
- [ ] Release of Test A data:	2024/4/20
- [ ] Registration deadline:	2024/6/20
- [ ] Release of test B data:	2024/6/28
- [ ] Evaluation results release and call for system reports and conference paper:	2024/7/5

## Reference
[1]  *Li, Bin*, *et al.* “Towards visual-prompt temporal answering grounding in medical instructional video.” *arXiv preprint arXiv:2203.06667 (2022).*

[2]  *Weng, Yixuan, and Bin Li.* “Visual Answer Localization with Cross-Modal Mutual Knowledge Transfer” [C]//ICASSP 2023-2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP). IEEE, 2023: 1-5.

[3]  *Deepak Gupta, Kush Attal, and Dina Demner-Fushman.* “A Dataset for Medical Instructional Video Classification and Question Answering.” *arXiv preprint arXiv:2201.12888, 2022.*

[4]  *Deepak Gupta, and Dina Demner-Fushman.* “Overview of the MedVidQA 2022 Shared Task on Medical Video Question-Answering*.* ” *BioNLP 2022@ ACL 2022 (2022): 264.*

[5]  *Zhang, Hao, et al.* “Natural language video localization: A revisit in span-based question answering framework.” *IEEE transactions on pattern analysis and machine intelligence 44.8 (2021): 4252-4266.*

[6]  *Li, Bin, et al.* “Learning To Locate Visual Answer In Video Corpus Using Question” [C]//ICASSP 2023-2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP). IEEE, 2023: 1-5.
