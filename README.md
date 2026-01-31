##Document Intelligence System using LayoutLMv3
Overview

This project builds an end-to-end document understanding system that extracts structured information from scanned documents and forms using a multimodal transformer model.
The system combines text, layout, and visual features to understand document structure and convert it into machine-readable JSON.

The core model used is LayoutLMv3, fine-tuned for document token classification.

Problem Statement

Traditional OCR reads text but does not understand document structure such as headers, questions, and answers.
This project solves structured document understanding, enabling:

Automatic form processing

Information extraction from business documents

Conversion of semi-structured documents into structured data

Approach

The system treats document understanding as a token classification task.

Pipeline:

Document image is processed.

Words and bounding boxes are used as layout-aware input.

LayoutLMv3 combines:

Text embeddings

2D positional layout embeddings

Visual features from the image

Model predicts semantic labels for each token:

HEADER

QUESTION

ANSWER

Tokens are post-processed and merged into readable fields.

Final output is structured JSON.

Model

Model: LayoutLMv3
Task: Token Classification
Training Dataset: FUNSD (Form Understanding in Noisy Scanned Documents)

LayoutLMv3 is a multimodal transformer designed for document AI. It learns relationships between text and document layout, enabling structure-aware understanding.

Dataset

FUNSD dataset is used for supervised training.
It contains:

Scanned form images

Word-level bounding boxes

Semantic labels (question, answer, header)

This dataset is widely used for document understanding research.

Training

The model is fine-tuned using:

HuggingFace Transformers

PyTorch

Mixed precision training (FP16)

The classifier head is trained to map document tokens into structural categories.

Training results show steady loss reduction, indicating successful learning of document structure.

Inference

During inference:

Document is processed using the trained processor.

Model predicts labels for tokens.

Tokens are reconstructed into readable text.

Fields are grouped into structured output.

Example output format:

{
  "HEADER": "NEW COMPETITIVE PRODUCTS",
  "QUESTION": "DATE TIME MANUFACTURER ...",
  "ANSWER": "BOBBY MILLS, REGIONAL SALES MGR ..."
}

API Deployment

A FastAPI server is provided to serve the model as an inference API.

Endpoint:

POST /extract


Input: Document image
Output: Structured JSON

This enables integration into real-world document processing systems.

Repository Structure
train_layoutlmv3_funsd.ipynb   -> Model training notebook
inference.py                  -> Inference pipeline
app.py                        -> FastAPI server
test_client.py                -> API request example
requirements.txt              -> Dependencies

Key Skills Demonstrated

Multimodal deep learning

Transformer fine-tuning

Document AI

Layout-aware NLP

Token classification

Model serving with FastAPI

End-to-end ML system design

Future Improvements

Integrate OCR engine for real scanned documents

Add key-value extraction for invoices/receipts

Model optimization for faster inference

Deploy on cloud platform

Conclusion

This project demonstrates how multimodal transformers can be used to build intelligent document processing systems capable of understanding document structure beyond simple text extraction.
