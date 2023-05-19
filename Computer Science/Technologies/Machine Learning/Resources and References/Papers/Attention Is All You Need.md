https://arxiv.org/abs/1706.03762

# Overview
They are establishing a new model layer type that will attempt to remove the requirement for recurrent networks. As there has been signifiant memory constraint as the context frame increases. There is also some performance issues as typically RNN tend to not be parallelization. This leads to performance requirements and are all around not as performant. 

The propose Transformers can be more parallelization since they avoid the requirement for 

### Compared to Other Models: Extended Neural GPU, ByteNet, ConvS2S
The main issue is that the other models use convolutional neural networks. These become spares as their context points are further apart and can fail on them. The Transformer reduces the points by a constant and resolves this issue, though this leads to some minor lower resolution, Multi-Head Attention to counteract.




@misc{vaswani2017attention,
      title={Attention Is All You Need}, 
      author={Ashish Vaswani and Noam Shazeer and Niki Parmar and Jakob Uszkoreit and Llion Jones and Aidan N. Gomez and Lukasz Kaiser and Illia Polosukhin},
      year={2017},
      eprint={1706.03762},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}