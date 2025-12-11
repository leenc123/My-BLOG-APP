---
title: Flutter打包脚本
tags: [flutter,shell]
categories: [移动开发,Flutter]
---
# 通用构建脚本
    ```bash
    #!/bin/bash
    set -e
    echo "🚀 开始 Flutter APK 打包..."
    # 定义变量
    BUILD_NAME=${1:-"1.0.0"}
    BUILD_NUMBER=${2:-"1"}
    OUTPUT_DIR="./builds"
    TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
    # 创建输出目录
    mkdir -p $OUTPUT_DIR
    echo "📦 构建配置:"
    echo "  - 版本号: $BUILD_NAME"
    echo "  - 构建号: $BUILD_NUMBER"
    echo "  - 输出目录: $OUTPUT_DIR"
    # 清理和准备
    echo "🧹 清理构建缓存..."
    flutter clean
    flutter pub get
    # 构建 APK
    echo "🔨 开始构建 APK..."
    flutter build apk --release \
        --build-name=$BUILD_NAME \
        --build-number=$BUILD_NUMBER \
        --obfuscate \
        --split-debug-info=./debug-info
    # 复制 APK 文件到根目录
    echo "📋 复制 APK 文件到指定目录..."
    APK_SOURCE_DIR="../build/app/outputs/flutter-apk"
    APK_FILES=$(find $APK_SOURCE_DIR -name "*.apk")
    for apk_file in $APK_FILES; do
        filename=$(basename "$apk_file")
        # 为文件名添加时间戳
        new_filename="${filename%.apk}_${TIMESTAMP}.apk"
        cp "$apk_file" "$OUTPUT_DIR/$new_filename"
        echo "  ✅ 已复制: $new_filename"
    done
    echo ""
    echo "🎉 打包完成！"
    echo "📱 APK 文件位置: $OUTPUT_DIR/"
    echo "📊 生成的文件:"
    ls -la $OUTPUT_DIR/*.apk 2>/dev/null || echo "  未找到 APK 文件"
    # 显示构建信息
    echo ""
    echo "📋 构建信息:"
    echo "  版本: $BUILD_NAME (Build $BUILD_NUMBER)"
    echo "  时间: $(date)"
    echo "  目录: $(pwd)/$OUTPUT_DIR"
    ```