Hello All !! First of welcome to this guide. This are my experinces with 3D image segmentation ,Vnet and caffe
...Hope they will be useful to you.
Lets get into topic
1. First to use Vnet ,which kind of data you have ? medical images(volumes) in 3D, lables (that too volume in 3D, created by some tool by hand)
2. Lables must be binary as we are using dice loss in Vnet
3. Hope you have saved this images either .mha,.mhd or nrrd format, as in Vnet it is used SITK ( you can change as per your need in datamanager class)
#so we are now ready with data
4. first download 3 D caffe
(https://github.com/faustomilletari/3D-Caffe)
5. Either do cmake or make to install and compile ,there is chance that after make runtest you may get error
 '''
 Check failed: ExactNumBottomBlobs() == bottom.size() (3 vs. 2) SoftmaxWithLoss Layer takes 3 bottom blob(s) as input.
 ## ExactNumBottomBlobs is set to be 3 in the loss_layer.hpp.
 '''
 'change it to 2 simple isn't it?'
'make sure you have installed 3D caffe correctly then you are ready to go'
6. then download Vnet from 
(https://github.com/faustomilletari/VNet)
7. go to main.py ,just create folder structure accordingly 
.. for example
 ..1. in train folder keep data
 ..1. subject123.mhd (main volume)
 ..1. subject123_segmentation.mhd(label volume)
 ..1. same for test folder
 ..1. subject456.mhd 
 ..1. subject456_segmentation.mhd' 
8. if you are using pycharm give system parameter ,-train or -test as per your need
9. if there is out of memory error coming then check 'nvidia-smi' if you are using GPU on server or reduce the data
10. Vnet converges early ,so I do not think we should train for 100000 iteration as I got nice results for 30000 then change step size
11. for more info check paper and close and open issues of Vnet .I will update this as I progress ahead with my experiments 
Thanks
