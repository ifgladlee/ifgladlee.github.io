---
layout: post
title: "emacsѧϰ�ʼ�֮buffer"
categories: notes
---

����Emacs�����ж��buffer��ÿ��buffer���и��Ե����֣������е����ļ��������еĲ�Ȼ������ʱ�̣�ֻ��һ��buffer�Ǳ�ѡ�еġ����emacsֻ��һ��window�������window���buffer��Ȼ���Ǳ�ѡ�е�״̬��������ж��window����ѡ�е�window���bufferΪ��ѡ�С�

- ������ѡ��buffers

  + `C-x b buffer RET`

    ѡ��򴴽�һ����������buffer��

  + `C-x 4 b buffer RET`

    ���ơ������Ƕ�����һ��window������

  + `C-x 5 b buffer RET`

    ���ƣ������Ƕ�����һ��frame������

  + `C-x LEFT/RIGHT`

    ѡ��ǰ/��һ��buffer.

  + `C-u M-g M-g`

    `C-u M-g g`

    ��ȡһ������n��������һ��window�д����һ��buffer�ĵ�n�С�

  +
- �г����ڵ�buffers

  + `C-x C-b`

    �г����ڵ�buffer�б�����`C-u C-x C-b`ֻ�г������ļ���buffers��

- ����buffer����

  + `C-x C-q`

    ���ص�ǰbuffer��ֻ��״̬��

  + `M-x rename-buffer RET name RET`

    ��������ǰbuffer��

  + `M-x rename-uniquely`

    ��������ǰbuffer����ĩβ����`<number>`��

  + `M-x view-buffer RET buffer RET`

    ��`buffer`�й��������

    `M-x rename-uniquely`���Զ�����ǰbuffer���ּ���һ�����ص�����ʹ֮���������ظ���

    ���⣬`M-x append-to-buffer`��`M-x insert-buffer`���Դ�һ��buffer�������ֵ���һ��buffer��

- ���buffer��

  + `C-x k bufname RET`

    ���`bufname`���buffer��

  + `M-x kill-some-buffer`

    ��һ���buffers��

  + `M-x kill-matching-buffers`

    ���ƥ��������ʽ��buffers��
