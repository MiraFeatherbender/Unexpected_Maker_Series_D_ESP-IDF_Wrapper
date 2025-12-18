if(CONFIG_EXAMPLE_COLORWHEEL)
    set(EXAMPLE_SRC "colorwheel.cpp")
elseif(CONFIG_EXAMPLE_BLINK)
    set(EXAMPLE_SRC "blink_example_main.cpp")
endif()

idf_component_register(
    SRCS
        "${EXAMPLE_SRC}"
        "UMSeriesD_idf.c"
        "UMSeriesD.cpp"
    INCLUDE_DIRS "."
)