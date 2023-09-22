# rust-llmops
some examples

```

[package]
name = "sentiment"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
rust-bert = "0.21.0"
clap = {version="4.4", features=["derive"]}
anyhow = "1.0"

/* Clap CLI for sentiment Analysis */
use clap::Parser;
use sentiment::classify;

#[derive(Parser)]
#[clap(version = "0.1.0", author = "Rust ML")]
struct Opts {
    #[clap(short, long, default_value = "I love you")]
    input: String,
}

fn main() {
    let opts: Opts = Opts::parse();
    classify(&opts.input).unwrap();
}



extern crate anyhow;
use rust_bert::pipelines::sentiment::SentimentModel;

pub fn classify(input: &str) -> anyhow::Result<()> {
    //    Set-up classifier
    let sentiment_classifier = SentimentModel::new(Default::default())?;

    let payload = vec![input];
    //    Run model
    let output = sentiment_classifier.predict(payload);
    println!("{output:?}");
    Ok(())
}


```