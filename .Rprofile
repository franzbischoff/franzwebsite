# nolint start
if (Sys.getenv("CI") == "") { # not CI
options(repos = c(CRAN = "https://cran.rstudio.org"))

if (.Platform$OS.type == "windows") {
  Sys.setenv(LC_CTYPE = "C")
}
}

source("renv/activate.R")

if (Sys.getenv("CI") == "") { # not CI

  if (Sys.getenv("RSTUDIO") == "") { # not in RStudio
    if (interactive()) {
      options(
        warnPartialMatchArgs = FALSE,
        warnPartialMatchDollar = FALSE,
        warnPartialMatchAttr = FALSE,
        usethis.protocol = "https",
        warn = 1 # warnings appear immediately, not in the end
        # error = recover
      )
      options(
        vsc.rstudioapi = TRUE,
        max.print = 1000,
        width = 200,
        vsc.show_object_size = TRUE,
        vsc.globalenv = TRUE,
        vsc.dev.args = list(width = 1000, height = 700)
      )

      options(languageserver.formatting_style = function(options) {
        style <- styler::tidyverse_style(scope = "tokens", indent_by = 2)
        style
      })

      suppressMessages(
        suppressWarnings({
          require("testthat", quietly = TRUE)
          require("devtools", quietly = TRUE)
          require("usethis", quietly = TRUE)
          require("conflicted", quietly = TRUE)
          require("here", quietly = TRUE)
          require("glue", quietly = TRUE)
        })
      )

      conflicted::conflict_prefer("filter", "dplyr")
      options(dplyr.summarise.inform = FALSE)

      if (.Platform$OS.type != "windows") {
        if (suppressMessages(requireNamespace("prettycode", quietly = TRUE))) {
          suppressMessages(prettycode::prettycode())
        }
      }
      if (Sys.getenv("RADIAN_VERSION") == "") {
        loadhistory() # if no file, no problem.

        # Cleaning up function
        .Last <- function() {
          savehistory() # comment this line if you don't want to save history
          cat("bye bye...\n") # print this so we see if any non-interactive session is lost here
        }
      }
    }
  } else { # in RStudio
        suppressMessages(
      suppressWarnings({
        require("testthat", quietly = TRUE)
        require("devtools", quietly = TRUE)
        require("usethis", quietly = TRUE)
        require("conflicted", quietly = TRUE)
        require("here", quietly = TRUE)
        require("glue", quietly = TRUE)
      })
    )

    conflicted::conflict_prefer("filter", "dplyr")
    options(dplyr.summarise.inform = FALSE)
  }
} else { # is CI
  message("Running .RProfile in CI")
}

options(
  blogdown.author = "Francisco Bischoff",
  blogdown.ext = ".Rmd", # Default extension of new posts: .md / .Rmd / .Rmarkdown
  # blogdown.filename.pre_processor = NA, # a function with one parameter (the title), to pre-process the filename
  blogdown.files_filter = blogdown:::filter_md5sum,
  blogdown.generator = "hugo",
  # blogdown.hugo.args = "--minify",
  # blogdown.hugo.dir = NA, # The directory of the Hugo executable
  # blogdown.hugo.server = c("-D", "-F", "--navigateToChanged", "--disableFastRender"),
  blogdown.hugo.version = "0.103.1",
  # blogdown.initial_files = NA,
  blogdown.insertimage.usebaseurl = FALSE, # RBloggers, https://github.com/rstudio/blogdown/blob/5aeb809c68cfa1a9e616bc9ed9878c3ea5d05300/NEWS.md#new-features-13
  blogdown.knit.on_save = FALSE,
  blogdown.knit.serve_site = FALSE,
  # blogdown.markdown.format = c("gfm", "+footnotes", "+tex_math_dollars", "+smart"),
  blogdown.method = "html", # The building method for R Markdown
  blogdown.rename_file = TRUE, # Rename file if the date is changed (metadata)
  blogdown.new_bundle = TRUE, # Create a new post in a bundle (new Hugo format)
  blogdown.protect.math = TRUE,
  # blogdown.publishDir = "../public_site", # The publish dir for local preview, to avoid RStudio for get busy tracking files
  blogdown.serve_site.startup = FALSE,
  blogdown.server.timeout = 30, # timeout in seconds for starting server
  blogdown.server.verbose = TRUE,
  # blogdown.server.wait = 2,
  # blogdown.site_root = NA,
  blogdown.subdir = "posts", # Default subdirectory under content/ for new posts
  blogdown.time = TRUE,
  # blogdown.subdir_fun = NA, # function. Update subdir in according to the title
  blogdown.time_diff = 0, # does html output file not exist, or is it older than Rmd for at least N seconds?
  blogdown.title_case = FALSE,
  blogdown.warn.future = TRUE,
  blogdown.widgetsID = TRUE, # Incremental IDs for HTML widgets, is only relevant if your website source is under version control and you have HTML widgets on the website.
  blogdown.yaml.empty = TRUE # Preserve empty fields in YAML
)

suppressMessages(library(blogdown))

# nolint end
