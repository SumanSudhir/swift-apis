add_library(TensorFlow SHARED
  BackwardsCompatibility.swift
  Context.swift
  Exports.swift
  Freezable.swift
  Initializers.swift
  Layer.swift
  Loss.swift
  StdlibExtensions.swift

  Bindings/EagerExecution.swift
  Bindings/RawOpsGenerated.swift
  Bindings/TFTensorOperation.swift
  Bindings/RawOpsAugmented.swift

  Core/ArrayOps.swift
  Core/CopyableToDevice.swift
  Core/DataTypes.swift
  Core/Device.swift
  Core/DifferentialOperators.swift
  Core/Execution.swift
  Core/LazyTensorContext.swift
  Core/LazyTensorOperation.swift
  Core/LazyTensorShapeInference.swift
  Core/LazyTensorTFFunctionBuilder.swift
  Core/LazyTensorTrace.swift
  Core/LazyTensorTraceCache.swift
  Core/BroadcastingPullback.swift
  Core/MixedPrecision.swift
  Core/PythonConversion.swift
  Core/Runtime.swift
  Core/Serialization.swift
  Core/ShapedArray.swift
  Core/StringTensor.swift
  Core/Tensor.swift
  Core/TensorGroup.swift
  Core/TensorHandle.swift
  Core/TensorShape.swift
  Core/Threading.swift
  Core/Utilities.swift

  Layers/Convolutional.swift
  Layers/Core.swift
  Layers/Dense.swift
  Layers/Dropout.swift
  Layers/Embedding.swift
  Layers/Initialization.swift
  Layers/Normalization.swift
  Layers/Pooling.swift
  Layers/Recurrent.swift
  Layers/Sequential.swift
  Layers/Upsampling.swift

  Operators/Basic.swift
  Operators/Comparison.swift
  Operators/Dataset.swift
  Operators/Image.swift
  Operators/LinearAlgebra.swift
  Operators/Math.swift
  Operators/NN.swift

  Optimizers/MomentumBased.swift
  Optimizers/Optimizer.swift
  Optimizers/SGD.swift)
set_target_properties(TensorFlow PROPERTIES
  OUTPUT_NAME swiftTensorFlow)
target_link_libraries(TensorFlow PRIVATE
  CTensorFlow
  Tensor)

get_swift_host_arch(swift_arch)
get_swift_host_os(swift_os)
install(TARGETS TensorFlow
  ARCHIVE DESTINATION lib/swift/${swift_os}
  LIBRARY DESTINATION lib/swift/${swift_os}
  RUNTIME DESTINATION bin)
if(CMAKE_SYSTEM_NAME STREQUAL Darwin)
  install(FILES $<TARGET_PROPERTY:TensorFlow,Swift_MODULE_DIRECTORY>/TensorFlow.swiftdoc
    DESTINATION lib/swift/${swift_os}/TensorFlow.swiftmodule
    RENAME ${swift_arch}.swiftdoc)
  install(FILES $<TARGET_PROPERTY:TensorFlow,Swift_MODULE_DIRECTORY>/TensorFlow.swiftmodule
    DESTINATION lib/swift/${swift_os}/TensorFlow.swiftmodule
    RENAME ${swift_arch}.swiftmodule)
else()
  install(FILES
    $<TARGET_PROPERTY:TensorFlow,Swift_MODULE_DIRECTORY>/TensorFlow.swiftdoc
    $<TARGET_PROPERTY:TensorFlow,Swift_MODULE_DIRECTORY>/TensorFlow.swiftmodule
    DESTINATION lib/swift/${swift_os}/${swift_arch})
endif()
